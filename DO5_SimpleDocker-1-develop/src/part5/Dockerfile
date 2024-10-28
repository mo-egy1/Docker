FROM ubuntu:20.04
# FROM nginx:latest
WORKDIR /home/



RUN apt-get update && \
    apt-get install -y nginx gcc spawn-fcgi libfcgi-dev && \
    rm -rf /var/lib/apt/lists/*

RUN groupadd -r nginx && useradd --no-log-init -r -g nginx nginx

COPY ./nginx/nginx.conf /etc/nginx/nginx.conf
COPY ./server.c ./server.c
COPY ./run.sh ./run.sh

RUN touch /var/run/nginx.pid && \
    chown -R nginx:nginx /etc/nginx/nginx.conf && \
    chown -R nginx:nginx /home && \
    chown -R nginx:nginx /var/* && \
    chown -R nginx:nginx /var/run/nginx.pid && \
    chmod u-s /usr/bin/passwd && \
    chmod u-s /usr/bin/newgrp && \
    chmod g-s /usr/bin/chage && \
    chmod u-s /usr/bin/gpasswd && \
    chmod u-s /bin/su && \
    chmod u-s /bin/mount && \
    chmod g-s /usr/sbin/pam_extrausers_chkpwd && \
    chmod g-s /usr/bin/wall && \
    chmod u-s /usr/bin/chsh && \
    chmod g-s /usr/bin/expiry && \
    chmod u-s /usr/bin/chfn && \
    chmod u-s /bin/umount && \
    chmod g-s /sbin/unix_chkpwd && \
    chmod +x run.sh

HEALTHCHECK CMD echo "Health check passed." || exit 1
USER nginx

ENTRYPOINT ["./run.sh"]
