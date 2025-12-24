############################
# Stage 1 – Prepare frontend
############################
FROM nginx:1.24 AS builder

# Remove default nginx config
RUN rm -f /etc/nginx/conf.d/default.conf

# Remove default html content
RUN rm -rf /usr/share/nginx/html/*

# Copy RoboShop nginx configuration
COPY nginx.conf /etc/nginx/nginx.conf

# Copy RoboShop frontend static files
COPY static/ /usr/share/nginx/html/

############################
# Stage 2 – Runtime
############################
FROM nginx:1.24

# Copy prepared nginx config and static files
COPY --from=builder /etc/nginx/nginx.conf /etc/nginx/nginx.conf
COPY --from=builder /usr/share/nginx/html /usr/share/nginx/html

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]
