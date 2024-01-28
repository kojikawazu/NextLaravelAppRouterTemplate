
## 全体的な確認ポイント

- 全プロジェクトディレクトリの権限がrootとなっていないこと

## Next.jsコンテナ側の確認ポイント

- webプロジェクトのディレクトリに「.env」ファイルが存在すること
- 「.env」が以下となっていること
  - NEXT_PUBLIC_BACKEND_URL=http://localhost:8000

```bash
# nextjsコンテナに入る
docker exec -it nextjs /bin/bash
# 疎通確認
ping laravel
```

## Laravelコンテナ側の確認ポイント

- serverプロジェクトのディレクトリに「.env」ファイルが存在すること
- 「.env」が以下となっていること
  - DB_CONNECTION=mysql
  - DB_HOST=mysql
  - DB_PORT=3306
  - DB_DATABASE=laravel
  - DB_USERNAME=root
  - DB_PASSWORD=root
- phpmyadminでアクセスし、laravelデータベースにuserテーブルが存在すること
  - (存在しない場合マイグレーション実行) 

```bash
# laravelコンテナに入る
docker exec -it laravel /bin/bash

# まずは疎通確認
ping mysql
# 次にmysqlコマンドによる確認
mysql -h mysql -u root -p
# 最後にアプリケーションによる接続確認
cd /var/www/html/server
php artisan tinker
DB::connection()->getPdo()
```