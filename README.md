# kubernetes
https://github.com/justmeandopensource/kubernetes/blob/master/docs/install-cluster-ubuntu-20.md

https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/install-kubeadm/
### After spinning up the Vagrant file you can create the Cluster manually

> 1. become root

	sudo su -

> 2. disable the Firewall

	ufw disable

> 3. disable SWAP

	swapoff -a; sed -i '/swap/d' /etc/fstab

> 4. Letting iptables see bridged traffic 

	cat <<EOF | sudo tee /etc/modules-load.d/k8s.conf
	br_netfilter
	EOF
	
	cat <<EOF | sudo tee /etc/sysctl.d/k8s.conf
	net.bridge.bridge-nf-call-ip6tables = 1
	net.bridge.bridge-nf-call-iptables = 1
	EOF
	sudo sysctl --system

> 5. Install docker

	{
	  apt update
	  apt install -y apt-transport-https ca-certificates curl gnupg-agent software-properties-common
	  curl -fsSL https://download.docker.com/linux/ubuntu/gpg | apt-key add -
	  add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
	  apt update
	  apt install -y docker-ce containerd.io
	}

> 6. Add kubernetes repository

	{
	  curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | apt-key add -
	  echo "deb https://apt.kubernetes.io/ kubernetes-xenial main" > /etc/apt/sources.list.d/kubernetes.list
	}

> 7. install kubernetes tools

	apt update && apt install -y kubeadm kubelet kubectl

> 8. Initialize Kubernetes Cluster (master only)

	kubeadm init --apiserver-advertise-address=192.168.1.151 --pod-network-cidr=10.0.0.0/16  --ignore-preflight-errors=all

> 9. Deploy Calico network driver

	kubectl --kubeconfig=/etc/kubernetes/admin.conf create -f https://docs.projectcalico.org/v3.14/manifests/calico.yaml

> 10. run kubectl commands as non-root user

	mkdir -p $HOME/.kube
	sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
	sudo chown $(id -u):$(id -g) $HOME/.kube/**config**

> 11. Cluster join command

	kubeadm token create --print-join-command # on master
	#run the command returned on workers

> 12. Enable kubectl autocompletion

	# as root
	kubectl completion bash >/etc/bash_completion.d/kubectl
	# as non root
	echo 'alias k=kubectl' >>~/.bashrc
	echo 'complete -F __start_kubectl k' >>~/.bashrc