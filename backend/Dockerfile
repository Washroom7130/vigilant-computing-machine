FROM maven:3.8.1-openjdk-17 AS builder
WORKDIR /app
COPY . .
RUN mvn clean package -DskipTests

FROM openjdk:17-jdk
WORKDIR /app

# Set the locale to UTF-8 for English and Vietnamese support
ENV LANG=en_US.UTF-8
ENV LANGUAGE=en_US:en
ENV LC_ALL=en_US.UTF-8

# Install locale package to ensure locales are generated
RUN apt-get update && apt-get install -y locales && \
    locale-gen en_US.UTF-8 && \
    apt-get clean

COPY --from=builder /app/target/*.jar app.jar
EXPOSE 5555
ENTRYPOINT ["java", "-Dfile.encoding=UTF-8", "-jar", "app.jar"]