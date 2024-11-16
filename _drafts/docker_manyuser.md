#Install docker

```
# yum install docker-engine
```

#Install docker-compose

```
# curl -L https://github.com/docker/compose/releases/download/1.7.1/run.sh > /usr/local/bin/docker-compose
# chmod +x /usr/local/bin/docker-compose
```

REBOOT

```
# docker-compose --version
# mkdir hello-world
# cd hello-world
# vi docker-compose.yml
    my-test:
        image: hello-world
```

```
wordpress:
  image: wordpress
  links:
    - wordpress_db:mysql
  ports:
    - 8080:80
    - 80:80
wordpress_db:
  image: mariadb
  environment:
    MYSQL_ROOT_PASSWORD: ScienceMag.Htm15
```



#Reference

[1] [Installation on CentOS](https://docs.docker.com/engine/installation/linux/centos/)

[2] [Install Compose](https://docs.docker.com/compose/install/)

[3] [docker/compose: Define and run multi-container applications with Docker](https://github.com/docker/compose)