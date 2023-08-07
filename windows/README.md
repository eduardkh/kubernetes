# K8s on Windows

> install minikube and helm

```powershell
choco install Minikube -y
choco install kubernetes-helm -y
choco install argocd-cli -y
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
argocd completion powershell >> $PROFILE
```

> interact with argocd (UI and CLI)

```powershell
# expose the API
kubectl port-forward svc/argo-cd-argocd-server -n argocd 8080:443
# get the initial password
kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d
# login with the CLI
argocd login --insecure localhost:8080 --username admin --password BXfN5p7HLTFcllms
# update the admin password
argocd account update-password --current-password BXfN5p7HLTFcllms --new-password lSDqksGA8e6cEi
```

> delete a kubernetes instance

```powershell
minikube status --profile=argo
minikube delete --profile=argo
```
