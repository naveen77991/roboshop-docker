############################
# Stage 1 – Build Stage
############################
FROM node:20-alpine AS builder

# App directory
WORKDIR /app

# Copy dependency files first (cache friendly)
COPY package*.json ./

# Install production dependencies
RUN npm install --only=production

# Copy application code
COPY server.js .

############################
# Stage 2 – Runtime Stage
############################
FROM node:20-alpine

# Create non-root roboshop user
RUN addgroup -S roboshop && adduser -S roboshop -G roboshop

# App directory
WORKDIR /app

# Copy app from builder stage
COPY --from=builder /app /app

# Change ownership
RUN chown -R roboshop:roboshop /app

# Switch to non-root user
USER roboshop

# App port
EXPOSE 8080

############################
# Frequently changing configs (KEEP AT BOTTOM)
############################
ENV MONGO=true
ENV REDIS_URL=redis://redis:6379
ENV MONGO_URL=mongodb://mongodb:27017/users

# Start users service
CMD ["node", "server.js"]
