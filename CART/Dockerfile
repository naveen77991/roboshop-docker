############################
# Stage 1 – Build stage
############################
FROM node:20-alpine AS builder

WORKDIR /app

# Copy dependency files first (cache)
COPY package*.json ./

# Install production dependencies
RUN npm install --only=production

# Copy application code
COPY server.js .

############################
# Stage 2 – Runtime stage
############################
FROM node:20-alpine

# Create non-root roboshop user
RUN addgroup -S roboshop && adduser -S roboshop -G roboshop

WORKDIR /app

# Copy app from builder
COPY --from=builder /app /app

# Change ownership
RUN chown -R roboshop:roboshop /app

# Switch to non-root user
USER roboshop

# App port
EXPOSE 8080

############################
# Frequently changing configs (BOTTOM)
############################
ENV REDIS_HOST=redis
ENV CATALOGUE_HOST=catalogue
ENV CATALOGUE_PORT=8080

# Start service
CMD ["node", "server.js"]
