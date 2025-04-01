# system stage
FROM node:18-alpine AS system
RUN addgroup -S appgroup && adduser -S appuser -G appgroup
USER appuser

# build stage
FROM system AS build
WORKDIR /app
COPY package.json .
RUN npm install
COPY . .
RUN npm run build

# runtime stage
FROM node:18-alpine
WORKDIR /app
RUN addgroup -S appgroup && adduser -S appuser -G appgroup
USER appuser
COPY --from=build /app ./
CMD ["npm", "run", "start"]
