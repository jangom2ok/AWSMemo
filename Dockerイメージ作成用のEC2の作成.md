## Dockerイメージ作成用のEC2の作成

### IAM管理画面でユーザを登録
次のポリシーを登録
- AmazonVPCFullAccess
- AmazonEC2FullAccess
- IAMReadOnlyAccess
- AmazonEC2ContainerRegistryFullAccess

### VPCの作成
単一のパブリックサブネットを持つ VPC を作成する。

### EC2を作成する
aws linux を選択

### EC2に接続

### yum のアップデート

```
sudo yum update
```
