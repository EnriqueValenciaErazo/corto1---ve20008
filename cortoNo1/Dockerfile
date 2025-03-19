FROM postgres:latest

ENV POSTGRES_USER: postgres
ENV POSTGRES_PASSWORD: postgres
ENV POSTGRES_DB: postgres


FROM maven:3.9.9-openjdk-23-slim AS build

WORKDIR /app

COPY mvnw .
COPY .mvn .mvn
COPY src /app/src
COPY pom.xml /app

RUN chmod +x mvnw
RUN ./mvnw clean package -DskipTests

FROM openjdk:23-jre-slim

WORKDIR /app
COPY --from=build /app/target/*.jar /app/app.jar
EXPOSE 8080
ENTRYPOINT ["java", "-jar", "app.jar"]

