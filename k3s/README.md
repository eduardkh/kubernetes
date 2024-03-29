# k3s on vagrant VM

> install

```bash
curl -sfL https://get.k3s.io | INSTALL_K3S_EXEC='--write-kubeconfig-mode=644 --node-ip=192.168.1.155 --flannel-iface=eth1' sh -
```

> check install

```bash
kubectl get all -A
```

> uninstall

```bash
/usr/local/bin/k3s-uninstall.sh
```

> k3s completion

```bash
k3s completion zsh > /usr/share/zsh/functions/Completion/Linux/_k3s
```

> make helm work with k3s and add completion

```bash
curl https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3 | bash
kubectl config view --raw > ~/.kube/config
chmod 600 ~/.kube/config
# as root
helm completion zsh > /usr/share/zsh/functions/Completion/Linux/_helm
```
