FROM mongo:7

# MongoDB init scripts folder ki copy cheyyali
COPY master.js /docker-entrypoint-initdb.d/


FROM mongo:7.0
COPY *.js /docker-entrypoint-initdb.d