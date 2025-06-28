FROM node:24-alpine

COPY . /opt/

WORKDIR /opt
# copy .env file- paste public ip in url
RUN npn install && \
    npn run build

RUN apk update && apk add apache2

RUN rm -rf /var/www/localhost/htdocs/* && \
    cp -rf dist/* /var/www/localhost/htdocs/

EXPOSE 80

CMD ["httpd","-D","FOREGROUND"]