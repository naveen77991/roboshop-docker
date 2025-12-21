FROM nginx:1.24

# Remove default nginx configuration
RUN rm -f /etc/nginx/conf.d/default.conf

# Remove default html content
RUN rm -rf /usr/share/nginx/html/*

# Copy RoboShop nginx configuration
COPY nginx.conf /etc/nginx/nginx.conf

# Copy RoboShop frontend static files
COPY static/ /usr/share/nginx/html/

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]
