FROM maven:3.9.9-eclipse-temurin-21 AS builder

WORKDIR /app

COPY pom.xml .

#for caching, this makes the container faster
RUN mvn dependency:go-offline -B

COPY src ./src

#packaging everything into single jar
RUN mvn clean package
#above we have built the code using single maven base image


#now we have the instruction, how to run our build code

FROM eclipse-temurin:21-jdk AS runner

WORKDIR /app

COPY --from=builder ./app/target/api-gateway-0.0.1-SNAPSHOT.jar ./app.jar

EXPOSE 4004

ENTRYPOINT ["java", "-jar", "app.jar"]


