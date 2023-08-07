# K8s on Windows

> install minikube and helm

```powershell
choco install Minikube -y
choco install kubernetes-helm -y
```

> spin up a kubernetes instance

```powershell
minikube up
```

> add completion in powershell

```powershell
kubectl completion powershell >> $PROFILE
helm completion powershell >> $PROFILE
```
