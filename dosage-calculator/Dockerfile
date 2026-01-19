# Use Java 17 base image
FROM eclipse-temurin:17-jdk

# Set working directory
WORKDIR /app

# Copy Gradle wrapper and config
COPY gradlew gradlew
COPY gradlew.bat gradlew.bat
COPY gradle gradle
COPY build.gradle settings.gradle ./

# Fix line endings + permissions, then download deps
RUN sed -i 's/\r$//' gradlew && chmod +x gradlew && ./gradlew dependencies

# Copy source code
COPY src src

# Build the application
RUN ./gradlew build

# Default command
CMD ["./gradlew", "test"]

