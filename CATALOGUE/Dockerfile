FROM node:20-alpine

WORKDIR /app

# 1️⃣ Copy only dependency files first (BEST PRACTICE)
COPY package*.json ./

# 2️⃣ Install dependencies
RUN npm install

# 3️⃣ Copy remaining application code
COPY . .

EXPOSE 8080

ENV MONGO=true
ENV MONGO_URL=mongodb://mongodb:27017/catalogue

CMD ["node", "server.js"]
