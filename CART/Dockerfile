FROM node:20-alpine

WORKDIR /app

# 1️⃣ Copy dependency file
COPY package.json ./

# 2️⃣ Install dependencies defined by developer
RUN npm install

# 3️⃣ Copy application code
COPY server.js ./

# Cart service environment variables
ENV REDIS_HOST=redis
ENV CATALOGUE_HOST=catalogue
ENV CATALOGUE_PORT=8080

CMD ["node", "server.js"]
