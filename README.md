# k8s Cluster on Proxmox 構築手順

## 目次

- [Versions](#versions)
- [前準備](#前準備)
  - [1. asdfをインストール](#1-asdfをインストール)
  - [2. それ以外のツールをasdf経由でインストール](#2-それ以外のツールをasdf経由でインストール)
- [k0sctl準備](#k0sctl準備)
- [ArgoCDのセットアップ](#argocdのセットアップ)
- [CephFSを用いたPVCの構築](#cephfsを用いたpvcの構築)
  - [関連記事](#関連記事)

## Versions

- asdf: v0.16.6
- k0sctl: v0.23.0
- k9s: v0.40.10
- helm: 3.17.2
- kubectl: 1.32.3
- argocd: 2.14.7

## 前準備

全部asdf経由でOK!

### 1. asdfをインストール: [手順](docs/asdf/README.md)

### 2. それ以外のツールをasdf経由でインストール

Pluginの追加方法: [手順](docs/asdf/README.md)

1. k0sctl
2. k9s
3. helm
4. kubectl
5. argocd

## k0sctl準備

1. k0sctl.ymlの作成 (`k0sctl init > k0ctl.yml`)
2. k0sctl.ymlの適用 (`k0sctl apply --config k0sctl.yml`)
3. kube configの取得 (`k0sctl kubeconfig > ~/.kube/config`)

## Helm VS ArgoCD

自分はArgocdでクラスタを観察したいので基本的にはArgocdで動作確認しています。
Helmも一応は動作するかとは思いますが、保証はできないことが多いです。
また、情報が古いこともあります。
うまくいかない場合はこのREADMEに拘らず、公式含め色々な情報を参考にしてください。

## ArgoCDのセットアップ

[手順](docs/argocd.md#install-argocd)

## CephFSを用いたPVCの構築

[手順](docs/proxmox-ceph-pvc/README.md)

### 関連記事

- [Proxmox × k0s × CephFS で構築するKubernetesストレージ基盤](https://zenn.dev/aobaiwaki/articles/28ad58a3acaf24)
- [kubernetesからProxmoxのCephを使う](https://www.tunamaguro.dev/articles/20240318-kubernetes%E3%81%8B%E3%82%89Proxmox%E3%81%AECeph%E3%82%92%E4%BD%BF%E3%81%86/)

## Minioのセットアップ

[手順](docs/minio/README.md)

## Harborのセットアップ

[手順](docs/harbor/README.md)

## Prometheus, Grafanaのセットアップ

以下でPrometheus, Grafanaをセットアップすることができますが、Promxmox Exporterで十分なのでなくても大丈夫です。

[手順](docs/monitoring/README.md)

1. helm Repoを追加
2. monitoring namespaceを作成
3. kube-prometheus-stackをインストール
4. Grafanaの初期パスワードを取得
5. `prometheus-grafana` ServiceをNodePortに切り替えてアクセス
