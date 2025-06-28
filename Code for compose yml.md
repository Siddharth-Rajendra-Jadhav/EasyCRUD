version: "3.8"
services:
  db:
    image: mariadb:latest
    ports:
      - 3306:3306
    environment:
      MYSQL_ROOT_PASSWORD: redhat
      MYSQL_DATABASE: student_db 
    volumes:
      - mariadb_data:/var/lib/mysql
  backend:
     build:
      context: ./backend
      dockerfile: Dockerfile
    ports:
      - 8080:8080
    depends_on: db
  frontend:
    build:
      context: ./frontend
      dockerfile: Dockerfile
    ports:
      - 80:80
    depends_on: backend
volumes:
  mariadb_data:


add+commit+push


On EC2
    - docker stop (container ID, container ID, container ID)
    - docker ps
    - git pull origin docker
    - cd EasyCRUD
    - docker compose up -d (to run the containers from compose.yml file)
    - docker compose down (to stop the containers from compose.yml file)