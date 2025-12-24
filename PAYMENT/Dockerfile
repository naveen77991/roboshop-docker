############################
# Stage 1 – Build stage
############################
FROM python:3.9-slim AS builder

WORKDIR /app

# Build tools for uwsgi
RUN apt-get update && \
    apt-get install -y gcc build-essential python3-dev && \
    rm -rf /var/lib/apt/lists/*

# Install dependencies
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

# Copy application code
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

# 🔥 COPY PYTHON PACKAGES & UWSGI BINARY
COPY --from=builder /usr/local /usr/local

# Copy application code
COPY --from=builder /app /app

EXPOSE 8080

CMD ["uwsgi", "--ini", "payment.ini"]
