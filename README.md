# k8s Cluster on Proxmox 構築手順

## 目次

- [Versions](#versions)
- [前準備](#前準備)
  - [1. asdfをインストール](#1-asdfをインストール)
  - [2. それ以外のツールをasdf経由でインストール](#2-それ以外のツールをasdf経由でインストール)
- [k0sctl準備](#k0sctl準備)
- [ArgoCDのセットアップ](#argocdのセットアップ)
- [Cloudflare Ingress Controllerのセットアップ](#cloudflare-ingress-controllerのセットアップ)
- [CephFSを用いたPVCの構築](#cephfsを用いたpvcの構築)
- [Cert Managerのセットアップ](#cert-managerのセットアップ)
- [Harborのセットアップ](#harborのセットアップ)
- [Cloudflareのセットアップ](#cloudflareのセットアップ)
- [Prometheus, Grafanaのセットアップ](#prometheus-grafanaのセットアップ)
- [Minioのセットアップ](#minioのセットアップ)
- [Nginx Ingress Controllerのセットアップ](#nginx-ingress-controllerのセットアップ)

## Versions

- asdf: v0.16.6
- k0sctl: v0.23.0
- k9s: v0.40.10
- helm: 3.17.2
- kubectl: 1.32.3
- argocd: 2.14.7

## 0. 前準備

### 1. asdfをインストール
  
[手順](docs/asdf/README.md)

### 2. asdf pluginの追加

[手順](docs/asdf/README.md)

それ以外の上記[Versions](#versions)に記載のツールをasdf pluginを用いてインストール


## k0sctl準備

1. k0sctl.ymlの作成 (`k0sctl init > k0ctl.yml`)
2. k0sctl.ymlの適用 (`k0sctl apply --config k0sctl.yml`)
3. kube configの取得 (`k0sctl kubeconfig > ~/.kube/config`)

## 1. ArgoCDのセットアップ

NodePortで一旦公開します。

[手順](docs/argocd/README.md)

## 2. Cloudflare Ingress Controllerのセットアップ

CloudflareのAPIを用いて、CloudflareのDNSを自動的に更新するIngress Controllerです。
これを用いることでどんなサービスもSSL化して公開することができます。

[手順](docs/cloudflare-ingress-controller/README.md)

## 1'. ArgoCDの本セットアップ

ArgoCD上にCloudflare Ingress Controllerをセットアップした後、Cloudflare Tunnel経由で公開します。

[手順](docs/argocd/README.md)

## 3. Rook Cephを用いたPVCの構築

[手順](docs/rook/README.md)

## 4. Cert Managerのセットアップ

Let's Encrypt + cert-manager + Cloudflare DNSで自動的に正式な証明書を発行します

[手順](docs/cert-manager/README.md)

## 5. Harborのセットアップ

[手順](docs/harbor/README.md)


## Minioのセットアップ (任意)

[手順](docs/minio/README.md)

## Nginx Ingress Controllerのセットアップ (任意)

[手順](docs/nginx/README.md)
