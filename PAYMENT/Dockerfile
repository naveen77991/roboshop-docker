############################
# Stage 1 – Builder
############################
FROM python:3.9-slim AS builder

WORKDIR /app

# Install OS deps (uwsgi + python headers)
RUN apt-get update && \
    apt-get install -y gcc python3-dev uwsgi uwsgi-plugin-python3 && \
    rm -rf /var/lib/apt/lists/*

# Install Python deps (WITHOUT uwsgi)
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

# Copy application code
COPY . .

############################
# Stage 2 – Runtime
############################
FROM python:3.9-slim

WORKDIR /app

# Runtime environment variables (UNCHANGED)
ENV CART_HOST=cart
ENV CART_PORT=8080
ENV USER_HOST=user
ENV USER_PORT=8080
ENV AMQP_HOST=rabbitmq
ENV AMQP_USER=roboshop
ENV AMQP_PASS=roboshop123

# Copy python libs + uwsgi binary safely
COPY --from=builder /usr/lib/uwsgi /usr/lib/uwsgi
COPY --from=builder /usr/bin/uwsgi /usr/bin/uwsgi
COPY --from=builder /usr/local /usr/local
COPY --from=builder /app /app

EXPOSE 8080

CMD ["uwsgi", "--ini", "payment.ini"]
