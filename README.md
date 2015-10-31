# WordPress (Docker on armhf)
Dockerized WordPress image running on armhf platform (ex: Raspberry Pi)

<div style="center;"><a href="https://asciinema.org/a/bk6fpi51c11otqmpqzj9m3ucs" target="_blank"><img src="https://asciinema.org/a/bk6fpi51c11otqmpqzj9m3ucs.png" width="500" /></a></div>

## Usage

```sh
λ ~/ mkdir wordpress && cd $_
λ ~/wordpress/ wget https://raw.githubusercontent.com/imZack/wordpress-armhf/master/docker-compose/docker-compose.yml
λ ~/wordpress/ docker-compose up
```

:tada: That's it. Now, just visit http://localhost:8080 :tada:

> You don't have docker-compose yet? Just hit `pip install docker-compose`.

## Data Persistence
In your docker-compose it will create two folder for you.
- `www-data` all WordPress data goes here.
- `mysql-data` all MariaDB data.

## FAQ

**How to fix file permissions?**

```sh
docker-compose run wordpress fix-permissions
```

**How to import current WordPress?**

1. Copy wordpress folder to `www-data` and execute `fix-permissions`.
2. Dump database data and `docker exec` import your dump.sql

**How to increase upload file size (modify php.ini)?**

1. Create `uploads.ini` file with these settings.
```ini
file_uploads = On
memory_limit = 128M
upload_max_filesize = 64M
post_max_size = 64M
max_execution_time = 1800
```

2. Edit `docker-compose.yml`, wordpress > volumes append `./uploads.ini:/usr/local/etc/php/conf.d/uploads.ini`

```
volumes:
 - ./www-data:/var/www/html
 - ./uploads.ini:/usr/local/etc/php/conf.d/uploads.ini
```

**More questions?**

[create an issue](https://github.com/imZack/wordpress-armhf/issues/new)

## Images
These images has been built for `armhf`.

Don't know How to run Docker on Raspberry Pi 2? [Check out Hypriot](http://blog.hypriot.com/downloads/)

### WordPress
Docker Hub:  [zack/wordpress-armhf:4.3.1-apache](https://hub.docker.com/r/zack/wordpress-armhf/)

[Dockerfile](https://github.com/imZack/wordpress-armhf/tree/master/wordpress)
> fork from official repo: [wordpress:4.3.1-apache](https://github.com/docker-library/wordpress/blob/4823a04099579f2aafb118ae8177449425cc84d2/apache/Dockerfile)

### MariaDB
Docker Hub: [armbuilds/mariadb](https://hub.docker.com/r/armbuilds/mariadb/)

Just use pre-build image from armbuilds

### PHP
Docker Hub: [zack/php-arm:5.6-apache](https://hub.docker.com/r/zack/php-armhf/)

[Dockerfile](https://github.com/imZack/wordpress-armhf/tree/master/php)

> fork from official repo: [php:5.6.14-apache](https://github.com/docker-library/php/blob/fec7f537f049aafd2102202519c3ca9cb9576707/5.6/apache/Dockerfile)

## Contributors

<table><tbody>
<tr><th align="left">YuLun Shih</th><td><a href="https://github.com/imZack">GitHub/imZack</a></td><td><a href="http://twitter.com/yuluntw">Twitter/@yuluntw</a></td></tr>
</tbody></table>
