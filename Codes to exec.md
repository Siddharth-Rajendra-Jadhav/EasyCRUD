#fork repository to git
#connect the git rep to visual studio code.

On EC2 create database-
    -install docker from docker site
    -install docker compose 
    run-
        - systemctl start docker
        - systemctl enable docker
        - git clone https://github.com/srj891/EasyCRUD.git
        - docker run -d -p 3306:3306 -e MYSQL_ROOT_PASSWORD=redhat -v mariadb_data:/var/lib/mysql/ mariadb
        - docker ps
        - docker exec -it (database ID) mariadb -uroot -predhat
        - create database student_db;
        - show databases;

        To check data-
            - show tables;
            - select * from user;
        
        - docker ps
        - docker inspect (container ID) | grep IP

In Visual Studio Code-
    Create branch to main as a name "docker"
    Backend-
    crete Dockerfile
        - FROM maven:3.8.3-openjdk-17
        - COPY . /opt/
        - WORKDIR /opt
        - RUN   rm -f src/main/resources/application.properties && \
                cp -f application.properties src/main/resources/application.properties && \
                mvn clean package-DskipTests
        - WORKDIR target/
        - EXPOSE 8080
        - ENTRYPOINT ["java","-jar"]
        - CMD ["student-registration-backend-0.0.1-SNAPSHOT.jar"]

    Copy application.properties file from srs-main-resources to backend.
    Open application.properties file from backend.
    change the IP to - 172.17.0.2, User - root

    save changes.

    ADD+COMMIT+PUSH+PUBLISH


On EC2-
    run-
        - cd EasyCRUD
        - cd backend
        - git checkout docker
        - docker build . -t backend:latest
        - docker images
        - docker volume list
        - docker run -d -p 8080:8080 backend:latest
        
        If error-
            - docker ps -a
            - docker logs (container ID)
            - chnage in Docker file of Visual studio code, then ADD+COMMIT+PUSH
            - git pull origin docker
            - docker build . -t backend:latest
            - docker run -d -p 8080:8080 backend:latest

        
In Visual Studio Code-
    Frontend-
    Create Dockerfile-
        - FROM node:24-alpine
        - COPY . /opt/
        - WORKDIR /opt
        - RUN npn install && \
              npn run build &&\
              apk update && apk add apache2 &&\
              rm -rf /var/www/localhost/htdocs/* && \
              cp -rf dist/* rf /var/www/localhost/htdocs/
        EXPOSE 80
        CMD ["httpd","-D","FOREGROUND"]

    open .env file - paste public IP in url.


On EC2-
    run-
        - cd EasyCRUD
        - cd frontend
        - git checkout docker
        - docker build . -t frontend:latest
        - docker images
        - docker volume list
        - docker run -d -p 80:80 backend:latest
        - docker ps
        - docker ps -a (to check all containers status)
        
        To stop/remove container-
            - docker stop (container ID, container ID, container ID)


Copy public ip and paste it in brower.
Add data.




