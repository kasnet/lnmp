![docker hub](https://img.shields.io/docker/pulls/kasnet/lnmp.svg?style=flat-square)
![docker hub](https://img.shields.io/docker/stars/kasnet/lnmp.svg?style=flat-square)

### Version
| Docker Tag | GitHub Release | Nginx Version | PHP Version | Alpine Version |
|-----|-------|-----|--------|--------|
| 7.1.12-fpm | Master Branch |1.13.7 | 7.1.12 | 3.4 |


### Links
- [https://github.com/kasnet/lnmp](https://github.com/kasnet/lnmp)
- [https://registry.hub.docker.com/u/kasnet/lnmp/](https://registry.hub.docker.com/u/kasnet/lnmp/)

## Quick Start
To pull from docker hub:
```
docker pull kasnet/lnmp:7.1.12-fpm
```
### Running
To run the container:
```
sudo docker run --name lnmp -p 88:80 -v src:/var/www/html -d kasnet/lnmp:7.1.12-fpm
```
To into the container:
```
sudo docker exec -it lnmp /bin/bash
```
