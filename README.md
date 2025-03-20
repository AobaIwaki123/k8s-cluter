# k8s Cluster構築手順

## Versions

- go: 1.24.1
- k0sctl: v0.23.0
- k9s: v0.40.10

## 前準備

全部asdf経由にすればよかった...

1. asdfインストール: [手順](docs/preliminaries.md#install-asdf)
2. asdf経由でgoインストール: [手順](docs/preliminaries.md#install-golang-with-asdf)
3. k0sctlインストール: [手順](docs/preliminaries.md#install-k0sctl)
4. k9sインストール: [手順](docs/preliminaries.md#install-k9s)
5. asdf経由でhelmインストール: [手順](docs/preliminaries.md#install-helm-with-asdf)

## k0sctl準備

1. k0sctl.ymlの作成 (`k0sctl init > k0ctl.yml`)
2. k0sctl.ymlの適用 (`k0sctl apply --config k0sctl.yml`)
3. kube configの取得 (`k0sctl kubeconfig > ~/.kube/config`)

## Prometheus, Grafanaのセットアップ

```sh
$ helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
$ helm repo update
```
