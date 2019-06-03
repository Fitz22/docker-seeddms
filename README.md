# Quick Start

## 1. start the container
~~~
docker run -d -ti \
	--name seeddms \
	-p 8082:80 \
	fit22/docker-seeddms:latest
~~~

## 2. basic setup
Assuming docker host's address is 172.17.0.1, use the following URL for basic setup:

`http://172.17.0.1:8082/install/`

Navigate to 'Start installation', select 'Create database tables' and press 'Apply'.
## 3. remove the install-trigger
~~~
docker exec -ti seeddms rm /var/www/seeddms51x/seeddms-5.1.10/conf/ENABLE_INSTALL_TOOL
~~~
and execute 
~~~
docker exec -ti seeddms chown -R www-data:www-data /var/www/
~~~
SeedDMS is ready to use now.


## 4. Access it via this URL:
`http://172.17.0.1:8082/`


# Some more commands
~~~
docker build -t seeddms:1 .

docker stop seeddms
docker rm seeddms

docker exec seeddms tar -C / -cf - /var/www/seeddms51x/ | xz > seeddms-backup.tar.xz
~~~


### mount volume outside container
~~~
docker run -d -ti \
	--name seeddms \
	--restart=always \
	-p 8082:80 \
	-v /dms/:/var/www/seeddms50x/ \
	-e SYSTEM_TIMEZONE="Europe/Berlin" \
	ludwigprager/docker-seeddms:latest
~~~

### open shell inside running container
~~~
docker exec -ti seeddms /bin/bash
~~~


### switch on install mode again
~~~
docker exec -ti seeddms touch /var/www/seeddms50x/seeddms-5.1.10/conf/ENABLE_INSTALL_TOOL
~~~
