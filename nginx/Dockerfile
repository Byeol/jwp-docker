FROM nginx

RUN apt-get update
RUN apt-get install -y wget

ENV DOCKERIZE_VERSION v0.2.0
RUN wget https://github.com/jwilder/dockerize/releases/download/$DOCKERIZE_VERSION/dockerize-linux-amd64-$DOCKERIZE_VERSION.tar.gz
RUN tar -C /usr/local/bin -xzvf dockerize-linux-amd64-$DOCKERIZE_VERSION.tar.gz

ADD default.tmpl /etc/nginx/sites-available/default.tmpl

CMD dockerize -template /etc/nginx/sites-available/default.tmpl:/etc/nginx/sites-available/default.conf -stdout /var/log/nginx/access.log -stderr /var/log/nginx/error.log -wait http://backend1:8080 -wait http://backend2:8080 -wait http://backend3:8080 -timeout 30s nginx -g "daemon off;"

RUN ln -fsv /etc/nginx/sites-available/default.conf /etc/nginx/conf.d/default.conf