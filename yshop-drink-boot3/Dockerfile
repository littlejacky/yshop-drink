# Stage 1: Build the application
FROM maven:3.9-eclipse-temurin-17 AS builder
WORKDIR /src
COPY . .
# Skip tests to speed up the build
RUN --mount=type=cache,target=/root/.m2 mvn clean package -DskipTests

# Stage 2: Run the application
FROM eclipse-temurin:17-jre
WORKDIR /yshop-server
# Copy the jar from the builder stage
COPY --from=builder /src/yshop-server/target/yshop-server.jar app.jar

ENV TZ=Asia/Shanghai
ENV JAVA_OPTS="-Xms512m -Xmx512m -Djava.security.egd=file:/dev/./urandom"
ENV ARGS=""

EXPOSE 48080

CMD java ${JAVA_OPTS} -jar app.jar ${ARGS}
