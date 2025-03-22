# Install Prometheus, Grafana with Helm

## Helm Repoを追加

```sh
$ helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
$ helm repo update
```

## monitoring namespaceを作成

```sh
$ kubectl create ns monitoring
```

##  kube-prometheus-stackをインストール

```sh
$ helm install prometheus prometheus-community/kube-prometheus-stack --namespace monitoring
$ kubectl --namespace monitoring get secrets prometheus-grafana -o jsonpath="{.data.admin-password}" | base64 -d ; echo
```
