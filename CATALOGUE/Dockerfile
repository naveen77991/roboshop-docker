############################
# Stage 1 – Build
############################
FROM node:20-alpine AS builder

WORKDIR /app

# Dependency layer (cached)
COPY package*.json ./
RUN npm install --only=production

# App code
COPY server.js .

############################
# Stage 2 – Runtime
############################
FROM node:20-alpine

# Create roboshop non-root user
RUN addgroup -S roboshop && adduser -S roboshop -G roboshop

WORKDIR /app

# Copy app from builder
COPY --from=builder /app /app

# Ownership to roboshop user
RUN chown -R roboshop:roboshop /app

# Switch to non-root user
USER roboshop

EXPOSE 8080

############################
# Frequently changing configs (KEEP AT BOTTOM)
############################
ENV MONGO=true
ENV MONGO_URL=mongodb://mongodb:27017/catalogue

CMD ["node", "server.js"]
