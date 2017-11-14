## docker-sonarqube-mysql
sonarqube with mysql server as dock

## create mouunt directory 

```
sudo mkdir -p /opt/docker/sonarqube
sudo mkdir -p /opt/docker/sonarqube/app
sudo mkdir -p /opt/docker/sonarqube/app/conf
sudo mkdir -p /opt/docker/sonarqube/app/data
sudo mkdir -p /opt/docker/sonarqube/app/logs
sudo mkdir -p /opt/docker/sonarqube/mysql
```

# create docker-compose.yml
```

version: '3'

services:
  mysql:
    image: mysql:5.7
    ports:
      - 3306:3306"
    environment:
      - MYSQL_ROOT_PASSWORD=root
      - MYSQL_DATABASE=sonarqube
    volumes:
      - /opt/docker/sonarqube/mysql

  sonarqube:
    image: sonarqube-docker
    ports:
      - "9000:9000"
    volumes:
      - /opt/docker/sonarqube/app/conf:/opt/sonarqube/conf
      - /opt/docker/sonarqube/app/data:/opt/sonarqube/data
      - /opt/docker/sonarqube/app/extensions:/opt/sonarqube/extensions
      - /opt/docker/sonarqube/app/logs:/opt/sonarqube/logs
    environment:
      - SONARQUBE_JDBC_URL=jdbc:mysql://mysql:3306/sonarqube?useUnicode=true&characterEncoding=utf8&rewriteBatchedStatements=true&useConfigs=maxPerformance
      - SONARQUBE_JDBC_USERNAME=sonarqube
      - SONARQUBE_JDBC_PASSWORD=sonarqube
      - DATABASE_PORT=3306
      - DATABASE_HOST=mysql
    links:
      - mysql
  ```


## run docker-compose
```
docker-compose up
```
