## Dockerイメージ作成

### 準備
Dockerイメージ作成環境(EC2)にて、work以下のファイルをコピーします。

```
scp ./work user@work_server:/work_directory_path/work
```

### ベースとなるDockerfileを作成する
以下のファイルにLAMP構成構築用の Dockerfile を書いています。

```
work/base/Dockerfile
```

Dockerfileの詳細は 基礎となるDockerイメージの作成.md を参照

### ビルド
Dockerfileのあるディレクトリで次のコマンドを実行します。

```
docker build [ -t ｛イメージ名｝ [ :｛タグ名｝ ] ] ./
```
