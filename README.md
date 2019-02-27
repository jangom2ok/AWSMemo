# AWS Lamp構成構築メモ

## はじめに
ここではオンプレミス1台構成(LAMP)のサーバをAWSへ移行する際の初めの手順として、AWSLinux上に、Dockerコンテナで作成する LAMPを構築する際の手順や予備知識などをメモとしてまとめています。

## AWSについて
AWSについての基本的な説明

## 疑問・用語解説
AWSを調べている中で疑問に思った内容や用語解説メモなど

## 環境構築手順
既にAWSアカウントを作成した状態からスタートします。構築手順の項目を以下に示します。

1. 作業用アカウントの作成
1. Dockerイメージ作成用のEC2の作成
1. Dockerイメージ作成環境構築
1. Dockerイメージ作成
1. ECRレポジトリの作成とDockerイメージの登録
1. 本番サーバのセットアップ
1. Docker Composeによる起動

## 参考URL
[【AWS】お名前.com で取得した独自ドメインを Amazon Route 53 で名前解決して EC2 インスタンスの Web サーバーにアクセスさせる手順](https://go-journey.club/archives/8340)

[Elastic Load Balancing で使用するインターネットゲートウェイを設定してアタッチする方法を教えてください。](https://aws.amazon.com/jp/premiumsupport/knowledge-center/attach-igw-elb/)

[AWS CLI Ubuntuへのインストール](https://qiita.com/yuyj109/items/3163a84480da4c8f402c)

