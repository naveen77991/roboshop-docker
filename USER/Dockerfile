############################
# Stage 1 – Build Stage
############################
FROM node:20-alpine AS builder

WORKDIR /app

COPY package*.json ./
RUN npm install --only=production

# 🔴 COPY ALL JS FILES (IMPORTANT)
COPY *.js .

############################
# Stage 2 – Runtime Stage
############################
FROM node:20-alpine

RUN addgroup -S roboshop && adduser -S roboshop -G roboshop

WORKDIR /app

COPY --from=builder /app /app
RUN chown -R roboshop:roboshop /app

USER roboshop

EXPOSE 8080

ENV MONGO=true
ENV REDIS_URL=redis://redis:6379
ENV MONGO_URL=mongodb://mongodb:27017/users

CMD ["node", "server.js"]
