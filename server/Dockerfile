# Use the official Maven image to build the project
FROM maven:3.9.1-eclipse-temurin-17 as build

WORKDIR /app

# Copy the pom.xml and download dependencies
COPY pom.xml .
RUN mvn dependency:go-offline

# Copy the source code and build the project
COPY src ./src
RUN mvn package -DskipTests

# Use an official OpenJDK runtime as a parent image
FROM eclipse-temurin:17-jdk-alpine

WORKDIR /app

# Copy the jar file from the build stage
COPY --from=build /app/target/*.jar app.jar

# Expose the port the app runs on
EXPOSE 8000

# Run the jar file
CMD ["java", "-jar", "app.jar"]
