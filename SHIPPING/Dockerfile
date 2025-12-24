FROM maven:3.9.6-eclipse-temurin-8

WORKDIR /app

# Copy dependency file
COPY pom.xml .

# Download dependencies
RUN mvn dependency:go-offline

# Copy source code
COPY src ./src

# Build application
RUN mvn clean package \
    && mv target/shipping-1.0.jar shipping.jar

# Runtime environment variables
ENV CART_ENDPOINT=cart:8080
ENV DB_HOST=mysql

CMD ["java", "-jar", "shipping.jar"]
