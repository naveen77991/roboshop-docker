FROM golang:1.20

WORKDIR /app

COPY main.go .

RUN go build -o dispatch main.go

EXPOSE 8080

CMD ["./dispatch"]
