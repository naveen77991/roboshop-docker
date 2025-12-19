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
ENV REDIS_HOST=redis
ENV CATALOGUE_HOST=catalogue
ENV CATALOGUE_PORT=8080

# Start catalogue service
CMD ["node", "server.js"]


