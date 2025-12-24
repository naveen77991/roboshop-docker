############################
# Stage 1 – Builder
############################
FROM python:3.9-slim AS builder

WORKDIR /app

# Build tools (for any python wheels)
RUN apt-get update && \
    apt-get install -y gcc python3-dev && \
    rm -rf /var/lib/apt/lists/*

# Install Python dependencies
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

# Copy application code
COPY . .

############################
# Stage 2 – Runtime
############################
FROM python:3.9-slim

WORKDIR /app

# 🔥 Install runtime dependencies (IMPORTANT)
RUN apt-get update && \
    apt-get install -y uwsgi uwsgi-plugin-python3 libexpat1 && \
    rm -rf /var/lib/apt/lists/*

# Application environment variables (UNCHANGED)
ENV CART_HOST=cart
ENV CART_PORT=8080
ENV USER_HOST=user
ENV USER_PORT=8080
ENV AMQP_HOST=rabbitmq
ENV AMQP_USER=roboshop
ENV AMQP_PASS=roboshop123

# Copy python libs + app code
COPY --from=builder /usr/local /usr/local
COPY --from=builder /app /app

EXPOSE 8080

CMD ["uwsgi", "--ini", "payment.ini"]
