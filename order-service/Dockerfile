# Stage 1: Build the application using Maven
FROM maven:3.9.9-eclipse-temurin-21 AS build

# Set the working directory
WORKDIR /workspace/app

# Copy the Maven project files
COPY pom.xml ./
COPY src ./src

# Build the project using Maven
RUN mvn clean package -DskipTests

# Stage 2: Create the runtime image
FROM eclipse-temurin:21

# Set the working directory
WORKDIR /workspace/app

# Copy the built JAR from the build stage
COPY --from=build /workspace/app/target/order-service-0.0.1-SNAPSHOT.jar /workspace/app/

# Expose the application port
EXPOSE 8080

# Run the application
CMD ["java", "-jar", "order-service-0.0.1-SNAPSHOT.jar"]
