# ---------- BUILD STAGE ----------
FROM maven:3.9.9-eclipse-temurin-21 AS builder

WORKDIR /build

COPY pom.xml .
COPY billing-service ./billing-service
COPY patient-service ./patient-service

RUN mvn clean package -pl patient-service -am -DskipTests

# ---------- RUNTIME STAGE ----------
FROM eclipse-temurin:21-jdk

WORKDIR /app

COPY --from=builder /build/patient-service/target/*.jar app.jar

EXPOSE 4000

ENTRYPOINT ["java","-jar","app.jar"]
