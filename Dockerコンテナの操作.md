## Dockerコンテナの操作

### 実行
```
docker run -i -t --name httpd イメージID
docker run -d -i -t -p 80:80 --name httpd イメージID
```

### 停止
```
docker stop
```

### Dockerコンテナへの接続
```
docker exec -it コンテナID /bin/bash
```
切断する場合は`exit`を使用する。

