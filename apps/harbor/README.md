TODO: 自前の Helm で管理する

## NameSpaceの作成

```sh
$ kubectl create ns harbor
```

## 証明書の追加

```sh
$ kubectl apply -f ./certificate.yaml -n harbor
```

## Argo CD の APP を起動

```sh
$ argocd app create --file ./harbor.yaml
```
