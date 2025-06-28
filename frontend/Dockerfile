FROM node:24-alpine

COPY . /opt/

WORKDIR /opt

.env file- paste public ip in url

RUN npn install && \
    npn run build &&\
    apk update && apk add apache2 &&\
    rm -rf /var/www/localhost/htdocs/* && \
    cp -rf dist/* /var/www/localhost/htdocs/
    
EXPOSE 80

CMD ["httpd","-D","FOREGROUND"]