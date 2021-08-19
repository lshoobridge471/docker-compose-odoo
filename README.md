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
Edit file and set ```DATABASE``` and ```ADDONS_PATH``` variables:
```
# Database to init ODOO.
DATABASE=example
# Custom addons path
ADDONS_PATH=/opt/my-custom-addons
```

Execute this server:
```sh
docker-compose up
```

Execute this server and detach:
```sh
docker-compose up -d
```