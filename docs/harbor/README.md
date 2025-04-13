# Install Harbor

```sh
$ argocd app create --file apps/harbor.yaml
```

## 2. テスト

- 初期パスワードの取得

```sh
$ kubectl get secret -n harbor harbor-core -o jsonpath="{.data.HARBOR_ADMIN_PASSWORD}" | base64 -d
Harbor12345
```

- 自己証明書をdockerに登録

```sh
$ sudo mkdir -p /etc/docker/certs.d/{実際のIP}:30003
$ kubectl get secret -n harbor harbor-nginx -o jsonpath="{.data.tls\.crt}" | base64 -d > harbor.crt
$ sudo cp harbor.crt /etc/docker/certs.d/{実際のIP}:30003/ca.crt
$ sudo systemctl restart docker
```

- ログイン

```sh
$ docker login {実際のIP}:30003
# 注意: Personal Access Tokenの使用が通常は推奨されています！
Username: admin
Password: Harbor12345
```

- イメージのプッシュ

```sh
$ docker pull alpine
$ docker tag alpine {実際のIP}:30003/library/alpine
$ docker push {実際のIP}:30003/library/alpine
```

- ブラウザで内容を確認
