# k8s Cluster構築手順

## Versions

- go: 1.24.1
- k0sctl: v0.23.0
- k9s: v0.40.10

## 前準備

1. asdfインストール
2. goインストール
3. k0sctlインストール
4. k9sインストール

## k0sctl準備

1. k0sctl.ymlの作成 (`k0sctl init > k0ctl.yml`)
2. k0sctl.ymlの適用 (`k0sctl apply --config k0sctl.yml`)
3. kube configの取得 (`k0sctl kubeconfig > ~/.kube/config`)
