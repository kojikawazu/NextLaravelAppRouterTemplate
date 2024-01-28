FROM php:8.1-fpm

RUN apt-get update && apt-get install -y \
    software-properties-common \
    libzip-dev \
    zip \
    unzip \
    git \
    vim \
    iputils-ping \
    default-mysql-client \
    && rm -rf /var/lib/apt/lists/* \
    && docker-php-ext-install pdo_mysql zip

# Composerのインストール
RUN curl -sS https://getcomposer.org/installer | php; \
    mv composer.phar /usr/local/bin/composer; \
    chmod +x /usr/local/bin/composer

# Laravelのインストール
RUN if [ ! -d "server" ]; then \
      # プロジェクトの立ち上げ
      composer create-project --prefer-dist laravel/laravel server; \
      cd server; \
      # Breezeのインストール
      composer require laravel/breeze --dev; \
      php artisan breeze:install api; \
      sed -i -e "s/^DB_PASSWORD=$/DB_PASSWORD=root/g" .env; \
      sed -i -e "s/^DB_HOST=127.0.0.1/DB_HOST=mysql/g" .env; \
      cd ../; \
    fi

# Laravelの起動
RUN cd server; \
    # DBマイグレーション
    php artisan migrate; \
    # キャッシュの削除
    php artisan cache:clear; \
    # キャッシュの再生成
    php artisan config:cache

# 開発サーバーの起動コマンド
CMD cd server; \
    php artisan cache:clear; \
    php artisan config:cache; \
    php artisan serve --host=0.0.0.0 --port=8000