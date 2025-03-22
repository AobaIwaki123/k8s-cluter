# k8s Cluster構築手順

## Versions

- asdf: v0.16.6
- k0sctl: v0.23.0
- k9s: v0.40.10
- helm: 3.17.2
- kubectl: 1.32.3
- argocd: 2.14.7

## 前準備

全部asdf経由でOK!

### 1. asdfをインストール: [手順](docs/adsf/README.md)

### 2. それ以外のツールをasdf経由でインストール

Pluginの追加方法: [手順](docs/adsf/README.md)

1. k0sctl
2. k9s
3. helm
4. kubectl
5. argocd

## k0sctl準備

1. k0sctl.ymlの作成 (`k0sctl init > k0ctl.yml`)
2. k0sctl.ymlの適用 (`k0sctl apply --config k0sctl.yml`)
3. kube configの取得 (`k0sctl kubeconfig > ~/.kube/config`)

## ArgoCDのセットアップ

[手順](docs/argocd.md#install-argocd)

## Minioのセットアップ

~~[手順](docs/minio.md#install-minio-with-argocd)~~

## Harborのセットアップ

[工事中](harbor/README.md)

## CephFSを用いたPVCの構築

[工事中](ceph-pvc/README.md)

## Prometheus, Grafanaのセットアップ

以下でPrometheus, Grafanaをセットアップすることができますが、Promxmox Exporterで十分なのでなくても大丈夫です。

[手順](docs/monitoring/README.md)

1. helm Repoを追加
2. monitoring namespaceを作成
3. kube-prometheus-stackをインストール
4. Grafanaの初期パスワードを取得
5. `prometheus-grafana` ServiceをNodePortに切り替えてアクセス
