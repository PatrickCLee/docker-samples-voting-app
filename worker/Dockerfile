# the original Dockerfile.j was outdated, thanks to chatGPT, below works!  2024-06-10

# Use Maven to build the application
FROM maven:3.8.4-openjdk-17-slim AS build
WORKDIR /app

# Copy the pom.xml and install dependencies
COPY pom.xml .
RUN mvn dependency:go-offline

# Copy the source code and build the application
COPY src ./src
RUN mvn package

# Use a minimal JRE to run the application
FROM openjdk:17-slim
WORKDIR /app

# Copy the built jar file from the build stage
COPY --from=build /app/target/worker-jar-with-dependencies.jar app.jar

# Run the application
CMD ["java", "-jar", "app.jar"]
