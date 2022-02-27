# Docker compose configuration file for Odoo with Postgres

Docker compose file to execute Odoo (with custom and enterprise addons) and PostgreSQL.

You will have installed [**docker-compose**](https://docs.docker.com/compose/install/).

Extra features:
- Custom environment file.

Instructions:
Copy .env.example to .env file:
```sh
cp .env.example .env
```
Edit file and set ```variables```:
```ini
# Versions
PG_VERSION=11
ODOO_VERSION=14.0

# Containers alias
ALIAS=project_alias

# Volumes config
PG_PATH=/home/user/volumes/postgresql
PG_LOGS_PATH=/home/user/volumes/postgresql-logs
ODOO_DATA_PATH=/home/user/volumes/odoo-data

# --- Odoo addons config
ODOO_EXTRA_ADDONS=/home/user/odoo-addons
ODOO_ENTERPRISE_ADDONS=/home/user/odoo-enterprise-addons
```

Configure `volumes/odoo/odoo.conf` file.
```sh
db_name = odoo
```

Execute this server:
```sh
docker-compose up
```

Close server:
```sh
ctrl+c
```

Execute this server and detach:
```sh
docker-compose up -d
```

Close detached server:
```sh
docker-compose down
```

View live odoo logs:
```sh
# Note: replace with your custom path
tail -f /home/user/volumes/odoo-data/odoo-server.log
```

Create new Odoo Module (scaffolding):
```sh
docker exec -it project_alias_odoo /usr/bin/odoo scaffold myaddonname /mnt/extra-addons
```

Run Odoo SHELL:
```sh
docker exec -it project_alias_odoo /usr/bin/odoo shell --db_host db -d odoo -w odoo
```
