# k8s Cluster on Proxmox 構築手順

自身に知識があまりないため、基本的に公式のHelmやValueを使ってArgoCDを構築しており、必要な時はvaluesを直接argocdのyamlに書き込んでいます。  
一区切り済んだらその辺りも勉強します！

## 目次

- [Versions](#versions)
- [前準備](#前準備)
  - [1. asdfをインストール](#1-asdfをインストール)
  - [2. それ以外のツールをasdf経由でインストール](#2-それ以外のツールをasdf経由でインストール)
- [k0sctl準備](#k0sctl準備)
- [ArgoCDのセットアップ](#argocdのセットアップ)
- [CephFSを用いたPVCの構築](#cephfsを用いたpvcの構築)
  - [関連記事](#関連記事)
- [Minioのセットアップ](#minioのセットアップ)
- [Cert Managerのセットアップ](#cert-managerのセットアップ)
- [Nginx Ingress Controllerのセットアップ](#nginx-ingress-controllerのセットアップ)
- [Harborのセットアップ](#harborのセットアップ)
- [Cloudflareのセットアップ](#cloudflareのセットアップ)
- [Prometheus, Grafanaのセットアップ](#prometheus-grafanaのセットアップ)

## Versions

- asdf: v0.16.6
- k0sctl: v0.23.0
- k9s: v0.40.10
- helm: 3.17.2
- kubectl: 1.32.3
- argocd: 2.14.7

## 前準備

全部asdf経由でOK!

### 1. asdfをインストール
  
[手順](docs/asdf/README.md)

### 2. asdf pluginの追加

[手順](docs/asdf/README.md)

それ以外の上記[Versions](#versions)に記載のツールをasdf pluginを用いてインストール


## k0sctl準備

1. k0sctl.ymlの作成 (`k0sctl init > k0ctl.yml`)
2. k0sctl.ymlの適用 (`k0sctl apply --config k0sctl.yml`)
3. kube configの取得 (`k0sctl kubeconfig > ~/.kube/config`)

## Helm VS ArgoCD

自分はArgocdでクラスタを観察したいので基本的にはArgocdで動作確認しています。
Helmも一応は動作するかとは思いますが、保証はできないことが多いです。
また、情報が古いこともあります。
うまくいかない場合はこのREADMEに拘らず、公式含め色々な情報を参考にしてください。

## ArgoCDのセットアップ (推奨)

[手順](docs/argocd/README.md)

## Rook Cephを用いたPVCの構築 (推奨)

[手順](docs/rook/README.md)

### 関連記事

- [Proxmox × k0s × CephFS で構築するKubernetesストレージ基盤](https://zenn.dev/aobaiwaki/articles/28ad58a3acaf24)
- [kubernetesからProxmoxのCephを使う](https://www.tunamaguro.dev/articles/20240318-kubernetes%E3%81%8B%E3%82%89Proxmox%E3%81%AECeph%E3%82%92%E4%BD%BF%E3%81%86/)

## Cert Managerのセットアップ (推奨)

Let's Encrypt + cert-manager + Cloudflare DNSで自動的に正式な証明書を発行する！  
インフラやってる感があって超かっこいい！ (小並感)
Harborにログインするときに一々自己証明書を登録するのは明らかに体験が悪いので、これはかなりおすすめです。

[手順](docs/cert-manager/README.md)

## Cloudflare Ingress Controllerのセットアップ (推奨)

CloudflareのAPIを用いて、CloudflareのDNSを自動的に更新するIngress Controllerです。
Harborに安全にアクセスするためにあった方がいいです。

[手順](docs/cloudflare-ingress-controller/README.md)

## Harborのセットアップ (推奨)

[手順](docs/harbor/README.md)

## Cloudflareのセットアップ (推奨)

Harborをhttpsで公開するために必要です。

[手順](docs/cloudflare/README.md)

## Prometheus, Grafanaのセットアップ (任意)

以下でPrometheus, Grafanaをセットアップすることができますが、Promxmox Exporterで十分なのでなくても大丈夫です。

[手順](docs/monitoring/README.md)

## Minioのセットアップ (任意)

[手順](docs/minio/README.md)

## Nginx Ingress Controllerのセットアップ (任意)

[手順](docs/nginx/README.md)
