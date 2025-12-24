############################
# Stage 1 – Build stage
############################
FROM python:3.9-slim AS builder

WORKDIR /app

# Copy dependency file
COPY requirements.txt .

# Install dependencies into virtual location
RUN pip install --no-cache-dir -r requirements.txt

# Copy full application code
COPY . .

############################
# Stage 2 – Runtime stage
############################
FROM python:3.9-slim

WORKDIR /app

# Application environment variables (UNCHANGED)
ENV CART_HOST=cart
ENV CART_PORT=8080
ENV USER_HOST=user
ENV USER_PORT=8080
ENV AMQP_HOST=rabbitmq
ENV AMQP_USER=roboshop
ENV AMQP_PASS=roboshop123

# Copy everything from builder (SAFE)
COPY --from=builder /app /app

EXPOSE 8080

# Start payment service (UNCHANGED)
CMD ["uwsgi", "--ini", "payment.ini"]
