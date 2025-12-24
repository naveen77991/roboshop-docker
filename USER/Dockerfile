
FROM node:20-alpine

WORKDIR /app

# Copy dependency file
COPY package.json ./

# Install dependencies
RUN npm install

# Copy application code
COPY server.js ./

# 🔴 IMPORTANT FIX (DISABLE INSTANA)
ENV INSTANA_DISABLED=true

# Required environment variables
ENV MONGO=true
ENV MONGO_URL=mongodb://mongodb:27017/users
ENV REDIS_URL=redis://redis:6379

CMD ["node", "server.js"]
