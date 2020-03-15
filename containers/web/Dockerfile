FROM nginx:1.17-alpine

LABEL maintainer="nagait84 <@nagait84>"

# 設定ファイルを上書き
RUN rm -f /etc/nginx/conf.d/*
ADD ./containers/web/default.conf /etc/nginx/conf.d/default.conf

# nginxの起動
CMD /usr/sbin/nginx -g 'daemon off;' -c /etc/nginx/nginx.conf
