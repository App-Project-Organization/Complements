# Gladle
FROM gradle:7.5.1-jdk17-alpine AS builder

# Path
WORKDIR /app
COPY build.gradle .
COPY settings.gradle .
COPY gradle/ gradle/
COPY src src

RUN gradle build -x test

FROM openjdk:17-jdk-alpine AS transfer-microservice

# Install jar
WORKDIR /app
COPY --from=builder /app/build/libs/transfer-microservice-0.0.1-SNAPSHOT.jar /app/app.jar

WORKDIR /app
COPY certificados certificados

WORKDIR /app
COPY datadummy datadummy

ENTRYPOINT ["java", "-jar", "app.jar"]