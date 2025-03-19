# Stage 1: Build the application
FROM maven:3.9.9-eclipse-temurin-21 AS build

# Set the working directory
WORKDIR /app

# Copy the Maven project file (pom.xml)
COPY pom.xml .

# Download dependencies for offline use
RUN mvn dependency:go-offline -B

# Copy the rest of the application code
COPY . .

# Build the application and package it as a JAR (skip tests for now)
RUN mvn clean package -DskipTests

# Stage 2: Create the runtime image
FROM eclipse-temurin:21-jdk

# Set the working directory for the final image
WORKDIR /app

# Copy the JAR file from the build stage
COPY --from=build /app/target/*.jar /inventory-service.jar

# Expose the port that your app will run on (if necessary)
EXPOSE 8082

# Set the entry point to run the JAR file
ENTRYPOINT ["java", "-jar", "/inventory-service.jar"]
