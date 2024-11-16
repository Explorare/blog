docker images
docker rmi
docker save -o [filename] [image]

docker ps
docker export 2a646cb51226 > wordpress_16_05_22.tar
sftp -P 31415 -i exp_ssh  Explorare@104.131.150.251:wordpress.tar .


sudo docker load < wordpress.tar

tar -cvf tecmint-14-09-12.tar /home/tecmint/
tar -xvf public_html-14-09-12.tar -C /home/public_html/videos/

==========================BACKUP============================

#docker ps -a
#mkdir backups
#docker run -it --rm -v $(pwd):/backups --volumes-from=[Container ID] busybox
#cd /var/www/html
Confirm that you can see all the files to your webpages.
#ls
#tar -c . -f /backups/html.tar

#docker run -it --rm -v $(pwd):/backups --link=c2aa9a51c303:dz mariadb bash
#env
#mysql -u root -p -h $DZ_PORT_3306_TCP_ADDR
#show databases
#connect [database]
In this case the name of the database is wordpress.
#show tables
#exit
 mysqldump --host $DZ_PORT_3306_TCP_ADDR -u root -p wordpress > /backups/wordpress.sql



==========================RESTORE============================

#Install docker
    https://docs.docker.com/engine/installation/linux/centos/
#Install docker-compose
    sudo -i
    curl -L https://github.com/docker/compose/releases/download/1.8.0-rc2/docker-compose-`uname -s`-`uname -m` > /usr/local/bin/docker-compose
    chmod +x /usr/local/bin/docker-compose

Upload auth key to target server

    $scp -i exp_ssh -P 54 exp_ssh explorare@104.131.150.202:./backups

Download backups from origin server

    $scp -i exp_ssh -P 12450 Explorare@45.32.8.197:./backups/html.tar .


# docker run -it --rm -v $(pwd):/backups --link=c2aa9a51c303:dz mariadb bash
# env

  DZ_PORT_3306_TCP_PROTO=tcp
  DZ_PORT_3306_TCP=tcp://172.17.0.2:3306
  DZ_PORT_3306_TCP_PORT=3306
  DZ_ENV_MYSQL_ROOT_PASSWORD=ScienceMag.Htm15

#root@701c926c36b8:/# mysql -u root -p -h $DZ_PORT_3306_TCP_ADDR wordpress
Enter password:

MariaDB [wordpress]> source /backups/backups/wordpress.sql

#docker run -it --rm -v $(pwd):/backups --volumes-from=[Container ID] busybox

#cd backups
#cp html.tar /var/www/html/
#cd /var/www/html
#tar -xvf html.tar

==============================================================

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

================Data Volumes====================

#docker inspect bb7e91a1f2da | less

wordpress

 "Mounts": [
        {
            "Source": "/var/lib/docker/volumes/55c80506ce82dc2b9831780da6779c4740dd2d0a8c9ed11d20959d0916faba33/_data",

            e72d6af1d6febf1c4925364775bba2146b0eb95c3572043d95e54ca9925a7451

mariadb

"Source": "/var/lib/docker/volumes/dc093eaaac448d1c0cd4bb425edc2d49c896026fc300f63526521a94f631c01c/_data",

dc093eaaac448d1c0cd4bb425edc2d49c896026fc300f63526521a94f631c01c


[Docker Tutorial: Backing Up and Restoring MySQL and WordPress in Docker - YouTube](https://www.youtube.com/watch?v=2ZX3F-aFOxQ)