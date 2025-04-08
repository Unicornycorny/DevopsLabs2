FROM node:18-alpine AS build

WORKDIR /app

COPY package*.json ./

RUN npm install && npm cache clean --force

COPY . .

RUN npm run build

FROM nginx:alpine AS production

RUN rm -rf /usr/share/nginx/html/*

COPY --from=build /app/build /usr/share/nginx/html

RUN addgroup -g 1001 nginxgroup \
    && adduser -D -G nginxgroup -u 1001 nginxuser \
    && chown -R nginxuser:nginxgroup /var/cache/nginx /var/run /usr/share/nginx/html

USER nginxuser

CMD ["nginx", "-g", "daemon off;"]
