## ECRリポジトリ操作手順
レポジトリ作成から push, pull するまでの手順

#### ECRリポジトリを作成する
AWSコンソールからECRのサービスを選択し、リポジトリの名前を入力し、リポジトリを作成する。

#### プロフィール作成
aws cliを用いてECRリポジトリに対してpushやpullを行うためのプロフィールを作成する。
```
aws configure --profile プロフィール名
```

#### ECRにログインする
1. プロフィール名は最初の手順で作成したプロフィールの名前を入力する。
1. 下記コマンドを実行するとログイン用のコマンドが表示されるので、コピーして貼り付け実行する

```
aws ecr get-login --no-include-email --region ap-northeast-1 --profile プロフィール名
```

#### Dockerイメージの作成
下記のコマンドを実行する

```
docker build -t リポジトリURI .
```

リポジトリURIはECRコンソール画面から確認できる。リポジトリ名の右側にURIが表示されている。既存のイメージを使用する場合は、下記コマンドでリポジトリ名を変更する。

```
docker tag イメージid リポジトリURI
```


### ECRにpushする
下記コマンドでECRに対してのイメージのpushが完了する。

```
docker push リポジトリURI
```

#### ECRからイメージをpullする
下記コマンドでECRに対してのイメージのpullが完了する。

```
docker pull リポジトリURI
```

#### ECR用アカウントのポリシーについて
2019/02/12/時点では以下の3種類のポリシーが存在する
- `AmazonEC2ContainerRegistryFullAccess` ECRに対して**全てのアクセス権限**を持つ。
- `AmazonEC2ContainerRegistryPowerUser` ECRに対して**読み込み**と**書き込み**のアクセス権限を持つ。
- `AmazonEC2ContainerRegistryReadOnly` ECRに対してイメージの一覧表示やDocker cliを使用したイメージのpullなど**読み込み**のみのアクセス権限を持つ
