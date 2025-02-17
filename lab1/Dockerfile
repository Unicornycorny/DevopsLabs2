FROM alpine:latest

RUN apk update && apk add --no-cache nginx

RUN addgroup -S mynginxgroup \
    && adduser -S mynginxuser -G mynginxgroup

# Создаём папки и назначаем владельца
RUN mkdir -p /var/run/nginx \
    && mkdir -p /var/log/nginx \
    && mkdir -p /var/www \
    && mkdir -p /var/tmp/nginx/client_body \
    && mkdir -p /var/lib/nginx \
    && chown -R mynginxuser:mynginxgroup \
       /var/run/nginx \
       /var/log/nginx \
       /var/www \
       /var/tmp/nginx \
       /var/lib/nginx \
       /etc/nginx

EXPOSE 80

# Запуск под непривилегированным пользователем
USER mynginxuser

CMD ["nginx", "-g", "daemon off;"]
