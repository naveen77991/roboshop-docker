FROM node:20-alpine

WORKDIR /app

# Copy dependency file
COPY package.json ./

# Install dependencies defined by developer
RUN npm install

# Copy application code
COPY server.js ./

ENV MONGO=true
ENV MONGO_URL=mongodb://mongodb:27017/users
ENV REDIS_URL=redis://redis:6379

CMD ["node", "server.js"]
