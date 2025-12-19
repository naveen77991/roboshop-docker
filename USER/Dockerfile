FROM node:20

# App work directory
WORKDIR /app

# Dependencies first (best practice – layer cache)
COPY package*.json .
COPY server.js .
RUN npm install




# App port
EXPOSE 8080

# Mongo env vars
ENV MONGO=true
ENV REDIS_URL='redis://redis:6379'
ENV MONGO_URL="mongodb://mongodb:27017/users"

# Start catalogue service
CMD ["node", "server.js"]


