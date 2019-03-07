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

### AWS CLI による EC2の起動と停止


### EC2に接続
```
ssh -i key.pem
```

### yum のアップデート

```
sudo yum update
```
