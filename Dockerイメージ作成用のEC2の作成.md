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

### AWS CLI による EC2の起動
```
aws ec2 start-instances --instance-ids "i-xxxxxxxxxxxxxxxxx"
```

### AWS CLI による EC2の状態確認
```
aws ec2 describe-instance-status --instance-ids "i-xxxxxxxxxxxxxxxxx"
```
停止状態であれば空文字が返ってくる


### AWS CLI による EC2の起動完了待ち
```
aws ec2 wait instance-running --instance-ids "i-xxxxxxxxxxxxxxxxx"; echo "next command"
```

### AWS CLI による EC2の停止
```
aws ec2 stop-instances --instance-ids "i-xxxxxxxxxxxxxxxxx"
```

### EC2に接続と切断
セキュリティグループへSSHの接続を許可し、SSH終了後はセキュリティグループから設定を削除しておく
```
aws ec2 authorize-security-group-ingress --group-id $MYSECURITYGROUP --protocol tcp --port 22 --cidr $MYIP/32
ssh -i key.pem user@server
aws ec2 revoke-security-group-ingress --group-id $MYSECURITYGROUP --protocol tcp --port 22 --cidr $MYIP/32
```

### yum のアップデート

```
sudo yum update
```
