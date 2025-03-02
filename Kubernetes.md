## K8s (Kubernetes)

#### 1. Install on all nodes on Alpine
```
# A. Elevate your rights
su
# B. Turn off swap in the session
swapoff -a
# Turn off swap on upstart
  # Remark all rows with swap in /etc/fstab
  sed -i '/ swap / s/^/#/' /etc/fstab
  # check with
  cat /etc/fstab
  # If it didn't work, do it manually

# C. Install docker
# Add the community repo (change the version number!!) to the apk repo file /etc/apk/repositories
http://dl-cdn.alpinelinux.org/alpine/v3.21/community
# Install
apk add docker
rc-update add docker boot
service docker start

# D. Install Kubernetes
# Add repo (edge testing)
echo "http://dl-cdn.alpinelinux.org/alpine/edge/testing" >> /etc/apk/repositories
apk update
# Install (kubeadm, kubelet and kubectl)
apk add kubeadm kubelet kubectl
rc-update add kubelet boot
rc-update add kubelet default
service kubelet start
# Create a config file for sysctl, /etc/sysctl.d/k8s.conf
net.bridge.bridge-nf-call-iptables = 1
net.bridge.bridge-nf-call-ip6tables = 1
net.ipv4.ip_forward                 = 1
# Apply the changes (sysctl --system for non Alpine)
sysctl -p

```

#### 2. Install on the masternode on Alpine
```
# E. Initialise the cluster. Replace [IP network] with your network incl mask. Eg: 10.2.0.0/16
kubeadm init --pod-network-cidr=[IP network]
# copy the token for worker node joins

# F. Make a config file for the root user
mkdir -p $HOME/.kube
cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
chown $(id -u):$(id -g) $HOME/.kube/config

# G. Install CNI (network). In this case Calicio
# Install Calico network plugin (change version number !!, https://docs.tigera.io/calico/latest/getting-started/kubernetes/quickstart)
kubectl create -f https://raw.githubusercontent.com/projectcalico/calico/v3.29.1/manifests/tigera-operator.yaml
```

#### 3. Install Workernodes on Alpine
```
# E. Take the copy of the output in D on the masternode and past it into the worker node/s
# or run ON the masternode, copy the output of the command
kubeadm token create --print-join-command
```

#### 4. When there are two nodes
```
As the cluster nodes are usually initialized sequentially, the CoreDNS Pods are likely to all run on the first control plane node. To provide higher availability, please rebalance the CoreDNS Pods with kubectl -n kube-system rollout restart deployment coredns after at least one new node is joined.
```

#### 5. Install Helm
https://helm.sh/docs/intro/install/
```
# Install Helm. Download file from https://github.com/helm/helm/releases (CHANGE VERSION)
wget https://get.helm.sh/helm-v3.16.4-linux-386.tar.gz
# Unpack
tar -zxvf helm-v3.16.4-linux-386.tar.gz
# cp the file
su
cd /usr/bin
cp /home/[yourUser]/linux-386/helm ./
# Test
helm help
```

#### 6. Add-on on the master node
```
# Add kubernetes-dashboard repository
helm repo add kubernetes-dashboard https://kubernetes.github.io/dashboard/
# Install
helm upgrade --install kubernetes-dashboard kubernetes-dashboard/kubernetes-dashboard --create-namespace --namespace kubernetes-dashboard

```



#### Alternative CNI (Flannel instead for Calicio, more simple, less control/filters). Not tested!
```
  # Step G Alternative
  kubectl apply -f https://raw.githubusercontent.com/coreos/flannel/master/Documentation/kube-flannel.yml
```


#### Token
```
# See the token list and expiration times
kubeadm token list
# Create a token
kubeadm token create
# Create a token and the join command
kubeadm token create --print-join-command
# If you don't have the value of --discovery-token-ca-cert-hash, you can get it by running the following commands on the control plane node
cat /etc/kubernetes/pki/ca.crt | openssl x509 -pubkey  | openssl rsa -pubin -outform der 2>/dev/null | openssl dgst -sha256 -hex | sed 's/^.* //'


# Manually create a discovery Token CA cert Hash
openssl x509 -pubkey -in /etc/kubernetes/pki/ca.crt | openssl rsa -pubin -outform der 2>/dev/null | openssl dgst -sha256 -hex | sed 's/^.* //'

```

#### Join
```
# Command
kubeadm join <control-plane-host>:<control-plane-port> --token <token> --discovery-token-ca-cert-hash sha256:<hash>
# Example
sudo kubeadm join 192.168.122.195:6443 --token nx1jjq.u42y27ip3bhmj8vj --discovery-token-ca-cert-hash sha256:c6de85f6c862c0d58cc3d10fd199064ff25c4021b6e88475822d6163a25b4a6c
```
  

#### Different ways to Check swap
```
cat /proc/meminfo | grep wap
cat /proc/swaps
swapon -s
vmstat
```

#### Check docker
```
# Check version
docker version
# Check containers
docker ps
# Run a test (need internet connection)
docker run hello-world
```

#### Troubleshooting (verbose)
```
kubectl get nodes -v=10
netstat -tulp | grep kubectl
ps aux | grep kubectl
kubectl config view
kubectl get all -A

# From kubectl get nodes -v=10
# "Unhandled Error" err="couldn't get current server API group list: Get \"http://localhost:8080/api?timeout=32s\"
export KUBECONFIG=/etc/kubernetes/admin.conf

```

#### Check Kubernetes
```
rc-status
service kubelet status
kubectl cluster-info
crictl ps

kubectl get nodes
kubectl get all
kubectl events -A

kubectl get pods --all-namespaces
kubectl get pods -n calico-system

kubectl get storageclass
```

#### Remove nodes
```
# A. On the master - Migrate pods from the node
kubectl drain  <node-name> --delete-local-data --ignore-daemonsets
# B. On the master - Prevent a node from scheduling new pods use – Mark node as unschedulable
kubectl cordon <node-name>
# C. On the worker node - beforejoining a new master
kubeadm reset
```


#### Network IPs
```
# Node IPs
#   These are the IP addresses assigned to the nodes, physical or virtual machines, used for admin access
kubectl get nodes -o wide

# Pod IPs
#   These IPs are used for inter-Pod communication within the cluster
kubectl get ns
kubectl get pods -n <namespace> -o wide

# Cluster IP
#   If a service is created in the cluster to group these Pods, it will be assigned a ClusterIP
#   This is an internal IP address used by the service to balance incoming requests to its Pods.
#   ClusterIP allows in-cluster services and Pods to communicate with the service without knowing the individual Pod IPs
kubectl get svc <service-name> -n <namespace>

# Node port
#   To expose one of the services externally, a NodePort service can be used.
#   This opens a specific port on all nodes’ IPs, and any traffic sent to this port is forwarded to the service.
#   External clients can access the service by sending requests to any of the node’s IPs at the designated NodePort
kubectl get svc <service-name> -n <namespace>

# Exernal IPs (Not common)
#   If a service needs to be exposed with an external IP without using a LoadBalancer, it can be assigned an External IP.
#   This is less common and typically requires additional routing or NAT configuration on the network.
kubectl get svc -n <namespace>

# LoadBalancer IP
#   Using a LoadBalancer type service will provision an external IP from the external load balancer
#   Handles incoming traffic, distributing it across the Pods of the service, with a single IP
kubectl get svc <service-name> -n <namespace>
```

#### Others
```
watch kubectl get nodes
kubectl describe ns

kubctl describe [service/namespace] frontend
kubectl get svc kube-dns -n kube-system

```




