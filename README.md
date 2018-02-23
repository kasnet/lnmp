![docker hub](https://img.shields.io/docker/pulls/kasnet/lnmp.svg?style=flat-square)
![docker hub](https://img.shields.io/docker/stars/kasnet/lnmp.svg?style=flat-square)

### Version
| Docker Tag | GitHub Release | Nginx Version | PHP Version | Alpine Version | Mysql Version |
|-----|-------|-----|--------|--------|--------|
| latest | Master Branch |1.13.7 | 7.1.12 | 3.4 | 5.7 |


### Links
- [https://github.com/kasnet/lnmp](https://github.com/kasnet/lnmp)
- [https://registry.hub.docker.com/u/kasnet/lnmp/](https://registry.hub.docker.com/u/kasnet/lnmp/)

## Quick Start PHP
To pull from docker hub:
```
docker pull kasnet/lnmp
```
### Running
To run the container:
```
sudo docker run --name lnmp 
-p 88:80 
-v <project_path>/src:/var/www/html:rw 
-v <project_path>/conf/nginx/nginx.conf:/etc/nginx/nginx.conf:rw 
-v <project_path>/conf/nginx/vhosts/nginx-site.conf:/etc/nginx/sites-available/default.conf:rw
-d kasnet/lnmp
```
To into the container:
```
sudo docker exec -it lnmp /bin/bash
```

## Quick Start MSYQL
To pull from docker hub:
```
docker pull msyql:5.7
```

### Runing
To run the container:
```
docker run --name mysql -p 3306:3306 -e MYSQL\_ROOT\_PASSWORD=123456 -v <project_path>/mysql_data:/var/lib/mysql -v <project_path>/conf:/etc/mysql/conf.d -d mysql:5.7
```
To into the container:
```
sudo docker exec -it mysql /bin/bash
```
