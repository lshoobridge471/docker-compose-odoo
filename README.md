# Docker compose file for Odoo with Postgress
## docker-compose-odoo:0.1

Docker compose file to execute Odoo (with custom addons) and PostgreSQL.

You will have installed [**docker-compose**](https://docs.docker.com/compose/install/).

Extra features:
- Custom environment file.
- Custom database name.

Instructions:
Copy .env.example to .env file:
```sh
cp .env.example .env
```
Edit file and set ```variables```:
```ini
# --- Global config
# Versions
PG_VERSION=11
ODOO_VERSION=14.0
# Containers alias
ALIAS=myprojectalias
# --- PGSQL Config
PG_PATH=/home/user/postgresql
PG_LOGS_PATH=/home/user/postgresql-logs
# --- Odoo Config
# Extra/enterprise addons
ODOO_EXTRA_ADDONS=/home/user/odoo-addons
ODOO_ENTERPRISE_ADDONS=/home/user/odoo-enterprise-addons
# Custom data path
ODOO_DATA_PATH=/home/user/odoo-data
```

Create the folders specified in .env file:
```sh
# Note: replace /home/user for your custom user path.
mkdir /home/user/postgresql
mkdir /home/user/odoo-data
```

Configure `volumes/odoo/odoo.conf` file.
```sh
db_name = yourdbname
```

Execute this server:
```sh
docker-compose up
```

Execute this server and detach:
```sh
docker-compose up -d
```

Close server:
```sh
ctrl+c
```

Close detached server:
```sh
docker-compose down
```

Create new Odoo Module:
```sh
# CONTAINER_NAME = ALIAS_odoo14
# Example:
export $CONTAINER_NAME="myprojectalias_odoo14"
docker exec -it $CONTAINER_NAME /usr/bin/odoo scaffold my_custom_addon_name /mnt/extra-addons
```

Run Odoo SHELL:
```sh
# CONTAINER_NAME = ALIAS_odoo14
# Example:
export $CONTAINER_NAME="myprojectalias_odoo14"
# Database name specified in .env file.
export $DBNAME="dbname"
docker exec -it $CONTAINER_NAME /usr/bin/odoo shell --db_host db -d $DBNAME -w odoo
```

View live odoo logs:
```sh
# Note: replace with your custom path
tail -f /home/user/odoo-data/odoo-server.log
```
