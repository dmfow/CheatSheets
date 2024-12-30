## Install on Alpine

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
service kubelet start
# Create a config file for sysctl, /etc/sysctl.d/k8s.conf
net.bridge.bridge-nf-call-iptables = 1
net.bridge.bridge-nf-call-ip6tables = 1
net.ipv4.ip_forward                 = 1








# Different ways to Check swap
cat /proc/meminfo | grep wap
cat /proc/swaps
swapon -s
vmstat

