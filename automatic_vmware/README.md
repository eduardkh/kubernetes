# Kubernetes auto deploy

> on host (must have vagrant installed)

```bash
vagrant up --provider=vmware_desktop
# after the cluster is up
vagrant ssh master
# under admin user (master box) create .kube/config
mkdir -p $HOME/.kube
sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
sudo chown $(id -u):$(id -g) $HOME/.kube/config

# test the cluster
kubectl apply -f https://k8s.io/examples/application/deployment.yaml
kubectl describe deployment nginx-deployment
```

> for more follow the link

<https://kubernetes.io/docs/tasks/run-application/run-stateless-application-deployment/>

> add MetalLB v0.13.10 to the mix

[MetalLB installation](https://metallb.universe.tf/installation/)

```bash
# set mode to : "ipvs"
kubectl edit configmap -n kube-system kube-proxy

# or with a script #

# see what changes would be made, returns nonzero returncode if different
kubectl get configmap kube-proxy -n kube-system -o yaml | \
sed -e "s/strictARP: false/strictARP: true/" | \
kubectl diff -f - -n kube-system

# actually apply the changes, returns nonzero returncode on errors only
kubectl get configmap kube-proxy -n kube-system -o yaml | \
sed -e "s/strictARP: false/strictARP: true/" | \
kubectl apply -f - -n kube-system

# Installation By Manifest
kubectl apply -f https://raw.githubusercontent.com/metallb/metallb/v0.13.10/config/manifests/metallb-native.yaml

k apply -f ipaddresspool.yaml
k apply -f l2advertisement.yaml

# test type: LoadBalancer
kubectl create deployment nginx --image=nginx
kubectl expose deployment nginx --port=80 --type=LoadBalancer
```
