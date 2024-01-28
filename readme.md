# Next.js(AppRouter) + Laravelのテンプレート用
---

## Dockerコンテナの操作方法

プロジェクトのルートディレクトリ内でコマンドを実行してください

```bash
# Docker compose 起動
docker-compose up -d
# Docker compose 停止
docker-compose down
```

## 各コンテナの確認方法

各コンテナの確認方法は以下になります。これはローカル上の確認です。

- Next.jsコンテナはブラウザで以下アドレスに接続します。

```
http://localhost:3000
```

- Laravelコンテナはブラウザで以下アドレスに接続します。

```
http://localhost:8000
```

- phpmyadminコンテナはブラウザで以下アドレスに接続します。

```
http://localhost:3030
```

- LaravelからMySQLへの接続確認は以下コマンドを実行します。

```bash
cd ~/[プロジェクト直下]

# Dockerコンテナの起動確認
docker ps
# laravelコンテナへ接続
docker exec -it laravel /bin/bash
# 疎通確認
ping mysql
# MySQLクライアントによる接続確認
mysql -h mysql -u root -p
```