```sh
$ kubectl create ns cert-manager
```

```sh
$ kubectl apply -f https://github.com/cert-manager/cert-manager/releases/download/v1.17.1/cert-manager.crds.yaml -n cert-manager
```

```sh
$ argocd app create --file ./cert-manager.yaml
```

Permissions:
Zone → DNS → Edit

Zone Resources:
Include → Specific Zone →（対象のドメイン名を選択）

```sh
$ kubectl create secret generic cloudflare-api-token-secret \
  --from-literal=api-token=<your-cloudflare-api-token> \
  --namespace=cert-manager
```

```sh
$ kubectl apply -f ./clusterissuer-letsencrypt.yaml -n cert-manager
```

```sh
$ kubectl apply -f ./certificate.yaml
```

## Argo CD で見るブランチの切り替え

```sh
$ argocd app set rook-ceph --revision {branch_name}
```
