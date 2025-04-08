FROM nginx:alpine

RUN addgroup -g 1001 proxygroup \
    && adduser -D -G proxygroup -u 1001 proxyuser \
    && chown -R proxyuser:proxygroup /var/cache/nginx /var/run /etc/nginx /usr/share/nginx/html

USER proxyuser

WORKDIR /etc/nginx

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]
