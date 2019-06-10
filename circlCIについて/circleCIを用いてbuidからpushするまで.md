### circleCIを用いてDocker imageをbuildし、AWS ECR上のリポジトリにpushするまで

##### orbについて
- ジョブ、コマンド、Executor のような設定要素をまとめた共有可能なパッケージ。
- 必要な機能がひとまとめになっているのでconfigファイルの記述がとても楽になる。
- circleCI公式のパッケージもあるので安心して利用できるものもある。
- 今回は`circleci/aws-ecr@6.0.0`というcircleCI公式のパッケージを利用した。
- orbsはversion2.1からサポートされている機能なので、configファイルのversion:の記述には2.1を指定すること

##### 環境変数の設定
- まずcircleCI上で使用する環境変数の設定を行う
- [環境変数の設定と種類](https://medium.com/veltra-engineering/circleci-2-0-a0549c65bc3b)
    - 今回はプロジェクトに環境変数を設定した。
- 今回のテーマを達成するために設定が必要な環境変数
    1. AWS_ACCOUNT_ID (AWSアカウントのID)
    1. AWS_ACCESS_KEY_ID (アカウントのアクセスキーID)
    1. AWS_SECRET_ACCESS_KEY (アカウントのシークレットアクセスキー)
    1. AWS_REGION (リージョン)
    1. AWS_ECR_ACCOUNT_URL (ECRリポジトリのアカウントURL。xxxxxxx.xxx.ecr.ap-northeast-1.amazonaws.com の部分)
    1. ECR_REPO (リポジトリ名)
    1. REPO_TAG (タグ名)

##### Dockerfileについて
- gitプロジェクト内にDockerfileを置いておくこと。無い場合はエラーが出ます。

##### circleCIの実行
1. gitリポジトリに、`.circleci/config.yml`を配置する。`config.yml`のソースコードは以下に記載
    - ``` config.yml
        orbs:
            aws-ecr: circleci/aws-ecr@6.0.0
        version: 2.1

        workflows:
            pushTest:
                jobs:
                - aws-ecr/build-and-push-image:
                    name: 'build-test'
                    repo: '${ECR_REPO}'
                    tag: '${REPO_TAG}'
      ```
1. gitリポジトリにDockerfileを配置する。(このDockerfileからビルドされたイメージがpushされる。)
1. 環境変数の設定を終えた後、gitリポジトリにコミットを行う。
1. jobが実行される。
##### jobの内容
1. Spin up Environment - 環境変数の設定
1. Checkout code - .circleci/config.ymlを置いたリポジトリのcloneを作成
1. Install AWS CLI - AWS CLIのインストール
1. Configure AWS Access Key ID - アクセスキーIDの設定
1. Configure AWS Secret Access Key - シークレットアクセスキーの設定
1. Configure AWS default region - リージョンの設定
1. Log into Amazon ECR - ECRにログイン
1. Build docker image - Dockerイメージをビルドする
1. Push image to Amazon ECR - ビルドしたイメージをpushする
- 上記のjobは`circleci/aws-ecr@6.0.0`のorbの`build-and-push-image`jobを実行することで自動的に行われる。

##### config.ymlの補足
- ```
    workflows:
        pushTest:
            jobs:
            - aws-ecr/build-and-push-image:
                name: 'build-test'
                repo: '${ECR_REPO}'
                tag: pushtest
  ```
  - `name` circleCIに表示されるjob名
  - `repo` リポジトリ名(環境変数を使用)
  - `tag` pushしたイメージにつけられるタグ名

##### ECR上のイメージをpullする
1. 環境変数`ECR_REPO`を使用するイメージの存在するリポジトリに変更する。
1. Dockerfileに使用するイメージを記述する。
- 今回のorbsを使用したビルドの場合、jobがECRログイン->Dockerイメージをビルドする順番なので特に意識することなくリポジトリ上のイメージを使用することが出来た。