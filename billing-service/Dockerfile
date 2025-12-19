FROM maven:3.9.9-eclipse-temurin-21 AS builder

WORKDIR /app

COPY pom.xml .

#for caching all the depedency using pom.xml, this makes the container faster
RUN mvn dependency:go-offline -B

COPY src ./src

#packaging everything into single jar
RUN mvn clean package
#above we have built the code using single maven base image


#now we have the instruction, how to run our build code

FROM eclipse-temurin:21-jdk AS runner

WORKDIR /app

COPY --from=builder ./app/target/billing-service-0.0.1-SNAPSHOT.jar ./app.jar

#port on which billing service app runs on
EXPOSE 4001

#port on which gRPC server runs on
EXPOSE 9001

ENTRYPOINT ["java", "-jar", "app.jar"]


