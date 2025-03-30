
```sh
$ kubectl create ns harbor
```

```sh
$ kubectl apply -f ./certificate.yaml -n harbor
```

```sh
$ argocd app create --file ./harbor.yaml
```
