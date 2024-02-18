required tools: `kubectl` `kubectx` `kubens` `helm` `k3d` `argocd` `devspace` `yq` `jq`

```sh
k3d cluster create argocd-01 --agents=2
kubectl cluster-info
kubectl config use-context k3d-argocd-01
```

```sh
kubectl create namespace argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/core-install.yaml
watch kubectl get pods -n argocd
```

```sh
kubectl config set-context --current --namespace=argocd
argocd login --core
```

```sh
argocd admin dashboard
```

```sh
argocd app create bootstrap-experimental \
   --repo https://github.com/antonsalman/argo-test-repo.git \
   --path argocd/experimental \
   --dest-namespace argocd \
   --dest-server https://kubernetes.default.svc \
   --sync-policy automated
```

```sh
argocd app create bootstrap-staging \
   --repo https://github.com/antonsalman/argo-test-repo.git \
   --path argocd/staging \
   --dest-namespace argocd \
   --dest-server https://kubernetes.default.svc \
   --sync-policy automated
```

```sh
argocd app create bootstrap-production \
   --repo https://github.com/antonsalman/argo-test-repo.git \
   --path argocd/production \
   --dest-namespace argocd \
   --dest-server https://kubernetes.default.svc \
   --sync-policy automated
```