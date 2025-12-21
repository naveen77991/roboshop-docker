FROM python:3.9

WORKDIR /app

COPY requirements.txt .
RUN pip install -r requirements.txt

COPY payment.py .
COPY rabbitmq.py .
COPY payment.ini .

EXPOSE 8080

CMD ["python","payment.py"]
