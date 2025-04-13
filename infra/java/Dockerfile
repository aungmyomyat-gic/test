# ---------- Stage 1: Build ----------
    FROM eclipse-temurin:23-jdk AS builder

    WORKDIR /app
    
    # Copy Maven wrapper and build config
    COPY mvnw .
    COPY .mvn .mvn
    COPY pom.xml .
    
    RUN chmod +x mvnw
    
    # Copy source code
    COPY src ./src
    
    # Build the project
    RUN ./mvnw clean package -DskipTests
    
    # ---------- Stage 2: Runtime ----------
    FROM openjdk:23-slim AS runtime
    
    WORKDIR /app
    
    # Copy the built JAR
    COPY --from=builder /app/target/*.jar app.jar
    
    # Expose port (if needed)
    EXPOSE 8080
    
    # Run the app
    ENTRYPOINT ["java", "-jar", "app.jar"]
    