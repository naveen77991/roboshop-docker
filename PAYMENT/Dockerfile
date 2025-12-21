FROM python:3.9

WORKDIR /app

# Application environment variables (from systemd unit file)
ENV CART_HOST=cart
ENV CART_PORT=8080
ENV USER_HOST=user
ENV USER_PORT=8080
ENV AMQP_HOST=rabbitmq
ENV AMQP_USER=roboshop
ENV AMQP_PASS=roboshop123

# Install dependencies
COPY requirements.txt .
RUN pip install -r requirements.txt

# Copy application code
COPY . .

EXPOSE 8080

# Start payment service (Docker replaces systemd)
CMD ["uwsgi", "--ini", "payment.ini"]
