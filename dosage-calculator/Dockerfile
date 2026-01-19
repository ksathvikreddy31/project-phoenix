# Java 17 base image
FROM eclipse-temurin:17-jdk

# Set working directory
WORKDIR /app

# Copy Gradle wrapper & config
COPY gradlew gradlew
COPY gradlew.bat gradlew.bat
COPY gradle gradle
COPY build.gradle settings.gradle ./

# Fix Windows line endings & permissions
RUN sed -i 's/\r$//' gradlew && chmod +x gradlew && ./gradlew dependencies

# Copy source code
COPY src src

# Build application
RUN ./gradlew build

# Default command
CMD ["./gradlew", "test"]

