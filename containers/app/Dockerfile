FROM ruby:2.7-alpine3.11 as dev_mode

LABEL maintainer="nagait84 <@nagait84>"

# ビルド時の作業ディレクトリ
WORKDIR /app

# AlpineLinuxPackagesで必要そうなコマンドをインストール
RUN apk update && \
    apk upgrade && \
    apk add --update --no-cache \
        build-base \
        git \
        imagemagick \
        imagemagick-dev \
        libxml2-dev \
        libxslt-dev \
        mysql-client \
        mysql-dev \
        nodejs \
        ruby-dev \
        tzdata \
        yarn

# yarnインストールの実行(先にlockファイルをコピーしてバージョンを固定)
COPY package.json yarn.lock ./
RUN yarn install

# マルチステージビルドで本番用イメージを作成
FROM dev_mode as prod_mode

# Railsの秘密情報のマスターキー(docker build時にオプションで宣言する)
ARG RAILS_MASTER_KEY
ENV RAILS_MASTER_KEY ${RAILS_MASTER_KEY}
# 本番モードで起動する
ENV RAILS_ENV production

# アプリのソースをイメージ内にコピー
COPY ./ ./

RUN bundle install

# フロント用のライブラリのインストールと静的ファイルの作成
RUN rails yarn:install
RUN rails webpacker:compile

# コンパイル後、マスターキー情報はイメージから消しておく
ENV RAILS_MASTER_KEY=
