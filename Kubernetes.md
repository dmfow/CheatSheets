## K8s (Kubernetes)

#### Install on all nodes on Alpine
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

#### Install on the masternode on Alpine
```

# E. Initialise the cluster. Replace [IP network] with your network incl mask. Eg: 10.2.0.0/16
kubeadm init --pod-network-cidr=[IP network]
# F. Make a config file for the root user
mkdir -p $HOME/.kube
cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
chown $(id -u):$(id -g) $HOME/.kube/config

# G. Install CNI (network). In this case Calicio
# Install Calico network plugin (change version number !!, https://docs.tigera.io/calico/latest/getting-started/kubernetes/quickstart)
kubectl create -f https://raw.githubusercontent.com/projectcalico/calico/v3.29.1/manifests/tigera-operator.yaml


# Alternative CNI (Flannel, more simple, less control/filters). Not tested!
kubectl apply -f https://raw.githubusercontent.com/coreos/flannel/master/Documentation/kube-flannel.yml

```

#### Install Workernodes on Alpine
```

# E. ON the masternode, copy the output of the command
kubeadm token create --print-join-command

# F. Take the copy of the output in D on the masternode and past it into the worker node/s


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


