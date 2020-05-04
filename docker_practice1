# コンテナとイメージ

alpineイメージをpullする
docker image pull alpine

alpineイメージをrunする
docker container run alpine

コンテナ起動時に sleep コマンドを実行する
docker container run -d alpine /bin/sleep 100

コンテナでコマンドを実行したい　→  -it (ホストの標準入出力をコンテナの標準入出力にする)
docker container run -it alpine /bin/bash

static-siteイメージからコンテナでwebサーバを起動してみる
docker run --name hoge -e AUTHOR="Panda" -d -p 9980:80 seqvence/static-site

  --name: コンテナ名指定できるオプション
  -e: 環境変数設定
  -d: バックグラウンドで実行
  -p: ポートマッピング
→ アクセス http://localhost:9980


コンテナを停止する
docker container stop hoge


コンテナを起動する
docker container start hoge



# イメージをビルドしてみる
参考：
https://www.ogis-ri.co.jp/otc/hiroba/technical/docker/part2.html


1-0.事前準備
mkdir ~/tmp
cd ~/tmp

1-1 Dockerfile 作成

vim  Dockerfile

```
#ベースイメージ
FROM nginx
ENV AUTHOR=Docker 
WORKDIR /usr/share/nginx/html
COPY _index.html /usr/share/nginx/html 
#CMDは一つだけしか書けない！
CMD cd /usr/share/nginx/html && sed -e s/Docker/"$AUTHOR"/ _index.html > index.html ; nginx -g 'daemon off; '
```


vim _index.html

```
<!DOCTYPE html><html>
<head><meta charset="utf-8"></head>
<body>
<h1>Hello Docker!</h1>
</body>
</html>
```

1-2. ビルド
docker image build -t app:v1 .
これによって、ベースイメージから私のイメージ(app)がを作られる
-t  name:tag

1-3. イメージからコンテナを起動
docker run -d -p 8888:80 --name ap app:v1

1-4. 動作確認
http://localhost:8888


1-5. コンテナ停止
docker container stop ap


DockerHubにpush/pullする

参考:
https://www.ogis-ri.co.jp/otc/hiroba/technical/docker/part3.html


2-0. DockerGHubでアカウントを作成
user名：xxx
pw: yyy

2-1.ログイン
docker login

2-2. イメージにタグをつける
docker image tag app1:v1 obayumiko00/app1:v1

2-3. pushする
docker image push obayumiko00/app1:v1

