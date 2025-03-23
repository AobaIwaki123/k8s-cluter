# Setup Cert Manger

## 1. Install Cert Manager

```sh
$ kubectl create ns cert-manager
```

### 1-0. Install CRDs

```sh
$ kubectl delete -f https://github.com/cert-manager/cert-manager/releases/download/v1.17.1/cert-manager.crds.yaml -n cert-manager
```

### 1-1. Helm

```sh
$ helm repo add jetstack https://charts.jetstack.io
$ helm repo update
```

```sh
$ helm install cert-manager --namespace cert-manager --version v1.17.1 jetstack/cert-manager
```

### 1-2. ArgoCD

```sh
$ argocd app create --file apps/cert-manager.yaml
```
