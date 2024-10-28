FROM nginx:latest
WORKDIR /home/

COPY ./nginx/nginx.conf /etc/nginx/nginx.conf
COPY ./server.c ./server.c
COPY ./run.sh ./run.sh

RUN apt-get update && \
    apt-get install -y gcc spawn-fcgi libfcgi-dev gosu && \
    chmod +x run.sh

ENTRYPOINT ["./run.sh"]
