# Install argocd

## argocd namespaceを作成

```sh
$ kubectl create namespace argocd
```

## argocdをインストール

```sh
$ kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
```

## Ingressで公開するためにSSL リダイレクトを無効化

```sh
$ kubectl apply -n argocd -f manifests/argocd-cmd-params-cm.yml
```

## argocdのServiceをNodePortに変更

```sh
$ kubectl patch svc argocd-server -n argocd -p '{"spec": {"type": "NodePort"}}'
```


## argocdの初期パスワードを取得して更新

```sh
$ argocd admin initial-password -n argocd
gQz9mVAdH7UgkdyI
$ argocd login <ARGOCD_SERVER>
$ argocd account update-password
Current Password: gQz9mVAdH7UgkdyI
New Password: <NEW_PASSWORD>
Repeat New Password: <NEW_PASSWORD>
```

## Cloudflare Ingress Controllerで公開

```sh
$ kubectl apply -f manifests/ingress.yml
```
