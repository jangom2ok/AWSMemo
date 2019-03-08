## Dockerイメージ作成環境構築

### Docker をインストール

```
sudo yum install -y docker
```

### Dockerデーモンを起動
```
sudo service docker start
```

### Dockerグループにユーザーを追加
```
sudo usermod -a -G docker ec2-user
```
ユーザーが追加できたかどうか確認する

```
cat /etc/group | grep docker
```

### 一度ログアウトしてからログインして確認する

```
docker info
```

```
Containers: 0
 Running: 0
 Paused: 0
 Stopped: 0
Images: 0
・・・・・
Registry: https://index.docker.io/v1/
```
↑がでればOK

### docker-compose のインストール

#### 最新バージョンを確認し、サイトに書いているコマンドを実行
[https://docs.docker.com/compose/install/](https://docs.docker.com/compose/install/)

```
sudo curl -L "https://github.com/docker/compose/releases/download/1.23.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
```

#### docker-composeの実行権限を与える
```
sudo chmod +x /usr/local/bin/docker-compose
```

#### 確認
docker-compose --version
