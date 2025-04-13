TODO: ArgoCD化されていないのでいつかリプレイスする

## NameSpaceを作成

```sh
$ kubectl create ns cert-manager
```

## CRDを追加

```sh
$ kubectl apply -f https://github.com/cert-manager/cert-manager/releases/download/v1.17.1/cert-manager.crds.yaml -n cert-manager
```

## Argo CD の APP を起動

```sh
$ argocd app create --file ./cert-manager.yaml
```

## Cloudflare の API トークンを作成

### Permissions:

- Zone:DNS:Edit

### Zone Resources:

Include → Specific Zone →（対象のドメイン名を選択）

## Cloudflare の API トークンを Secret に登録

```sh
$ kubectl create secret generic cloudflare-api-token-secret \
  --from-literal=api-token=_MeiCg75YRIamLCjfEJubjRhiEvdqdnBY7YMIeAA \
  --namespace=cert-manager
```

## ClusterIssuer を作成

```sh
$ kubectl apply -f ./clusterissuer-letsencrypt.yaml
```

## Argo CD で見るブランチの切り替え

```sh
$ argocd app set cert-manager --revision {branch_name}
```
