FROM python:3.9-slim

WORKDIR /app

# Install ONLY required build dependencies
RUN apt-get update \
    && apt-get install -y gcc python3-dev \
    && rm -rf /var/lib/apt/lists/*

# Copy dependency file
COPY requirements.txt .

# Install python dependencies
RUN pip install --no-cache-dir -r requirements.txt

# Copy application code
COPY . .

# Environment variables (from your systemd service)
ENV CART_HOST=cart
ENV CART_PORT=8080
ENV USER_HOST=user
ENV USER_PORT=8080
ENV AMQP_HOST=rabbitmq
ENV AMQP_USER=roboshop
ENV AMQP_PASS=roboshop123

# Start payment service
CMD ["uwsgi", "--ini", "payment.ini"]
