# Nextcloud install with docker-compose & letsencrypt certificates

## Prerequisites

Create partitions (primary, logical or LVM) for /var/lib/nextcloud/app & /var/lib/nextcloud/db as ext4 filesystem and mount them
Write environment files as follow:

mariadb.env

```bash
MYSQL_ROOT_PASSWORD=xxx
```

db.env

```bash
MYSQL_DATABASE=xxx
MYSQL_USER=xxx
MYSQL_PASSWORD=xxx
```

nextcloud.env

```bash
NEXTCLOUD_ADMIN_USER=xxx
NEXTCLOUD_ADMIN_PASSWORD=xxx
```

## Install

Build images from latests versions (web, proxy & docker-gen) and launch stack

```bash
docker-compose build --pull
docker-compose up -d
```

Wait for all services to be up (mainly db and app)

```bash
docker-compose logs -f
```

Run db commands to fix warnings

```bash
docker-compose exec --user www-data app php occ db:add-missing-indices
docker-compose exec --user www-data app php occ db:convert-filecache-bigint
```

## Post install

Go to https://url_of_nextlcoud_instance/settings/admin, login with Nextcloud admin account and set correct parameters
