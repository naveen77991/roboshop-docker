# ---------- Build stage ----------
FROM maven:3.9-eclipse-temurin-17 AS build

WORKDIR /app

# copy pom first (for cache)
COPY pom.xml .
RUN mvn dependency:go-offline

# copy source
COPY src ./src

# build jar
RUN mvn clean package && mv target/shipping-1.0.jar shipping.jar


# ---------- Runtime stage ----------
FROM eclipse-temurin:17-jre

WORKDIR /app

# non-root user
RUN useradd --system --home /app --shell /sbin/nologin roboshop

COPY --from=build /app/shipping.jar shipping.jar
RUN chown -R roboshop:roboshop /app

USER roboshop

ENV CART_ENDPOINT=cart:8080
ENV DB_HOST=mysql

EXPOSE 8080

CMD ["java", "-jar", "shipping.jar"]
