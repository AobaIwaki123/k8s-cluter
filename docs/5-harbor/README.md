## 証明書の準備

- 証明書が発行されるまで長くて5分程度

```sh
$ kubectl apply -f manifests/certificate.yaml
```

## Install Harbor

```sh
$ argocd app create --file argocd/harbor.yaml
```

## 2. テスト

- 初期パスワードの取得

```sh
$ kubectl get secret -n harbor harbor-core -o jsonpath="{.data.HARBOR_ADMIN_PASSWORD}" | base64 -d
Harbor12345
```
