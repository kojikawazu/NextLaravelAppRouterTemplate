FROM node:latest

WORKDIR /app

RUN apt-get update && apt-get install -y \
    software-properties-common \
    libzip-dev \
    zip \
    unzip \
    git \
    vim \
    iputils-ping \
    && rm -rf /var/lib/apt/lists/*

RUN if [ ! -d "web" ]; then \
      git clone https://github.com/laravel/breeze-next.git web; \
      cd web; \
      rm -rf .git; \
      # 注意点：package.jsonは以下のようにする必要がある。
      # "scripts": {
    　#    "dev": "next dev -H 0.0.0.0 -p 3000",
      sed -i -e "s/\"dev\": \"next dev\"/\"dev\": \"next dev -H 0.0.0.0 -p 3000\"/" package.json; \
      cp -p .env.example .env; \
      cd ../; \
    fi

RUN cd web && npm install

# 開発サーバーの起動コマンド
CMD ["npm", "run", "dev", "--prefix", "web"]