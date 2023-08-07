# K8s on Windows

> install minikube and helm

```powershell
choco install Minikube -y
choco install kubernetes-helm -y
```

> spin up a kubernetes instance

```powershell
minikube up
# or
minikube start --cpus=4 --memory=4096 --driver=hyperv --profile=argo
```

> add completion in powershell

```powershell
minikube completion powershell >> $PROFILE
kubectl completion powershell >> $PROFILE
helm completion powershell >> $PROFILE
```

> delete a kubernetes instance

```powershell
minikube status --profile=argo
minikube delete --profile=argo
```
