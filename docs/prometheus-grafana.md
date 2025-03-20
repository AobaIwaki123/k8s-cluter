# Install Prometheus, Grafana with Helm

## Helm Repoを追加

```sh
$ helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
$ helm repo update
```

## monitoring namespaceを作成

```sh
$ kubectl create ns monitoring
$ kubectl config set-context --current --namespace=monitoring
```

##  kube-prometheus-stackをインストール

```sh
$ helm install prometheus prometheus-community/kube-prometheus-stack
$ kubectl --namespace monitoring get secrets prometheus-grafana -o jsonpath="{.data.admin-password}" | base64 -d ; echo
$ export POD_NAME=$(kubectl --namespace monitoring get pod -l "app.kubernetes.io/name=grafana,app.kubernetes.io/instance=prometheus" -oname)
  kubectl --namespace monitoring port-forward $POD_NAME 3000
```
