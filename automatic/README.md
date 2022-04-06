# Kubernetes auto deploy


> on host (must have vagrant installed)

```bash
vagrant up
# after the cluster is up
vagrant ssh master
```

> under admin user master box create .kube/config

```bash
mkdir -p $HOME/.kube
sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
sudo chown $(id -u):$(id -g) $HOME/.kube/config

# test the cluster
kubectl apply -f https://k8s.io/examples/application/deployment.yaml
kubectl describe deployment nginx-deployment
```

>for more follow the link

<https://kubernetes.io/docs/tasks/run-application/run-stateless-application-deployment/>
