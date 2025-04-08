FROM openjdk:17-alpine AS build

WORKDIR /app

COPY pom.xml ./

RUN apk --no-cache add curl \
    && echo "Загружаем зависимости..." \
    && <команда для предзагрузки зависимостей, зависит от Maven или Gradle> \
    && rm -rf /var/cache/apk/*

COPY src/ ./src/

RUN <команда сборки, например> mvn clean package -DskipTests=true

FROM openjdk:17-alpine

RUN addgroup -g 1001 springgroup \
    && adduser -D -G springgroup -u 1001 springuser

USER springuser

WORKDIR /app

COPY --from=build /app/target/your-app.jar ./app.jar

EXPOSE 8080

ENTRYPOINT ["java", "-jar", "app.jar"]
