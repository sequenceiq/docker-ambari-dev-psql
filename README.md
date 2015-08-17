# Postgres with pre-initiaized ambari database schema
While developing Ambari Server we may want to quickly set up a postgres database pre-initiaized with Ambari database schema. This docker image sets up a postgres database with 'ambari' database user and latest database schema from 'trunk' branch by default.


## Starting the container
This will start an image based on postgres and pre-installed ambari database. The ambari database schema is created based on trunk.

```
docker run -d -P --name amabri-dev-psql-trunk sequenceiq/ambari-dev-psql
```

Explanation of the parameters:
- **-d**: run as daemon
- **-P**: since the Postgres database running within the container listens on the default port 5432 this needs to be exposed so as it'd reachable from outside of the container
- **--name**: sets the container name to **amabri-dev-psql-trunk** (optional)

## Starting the container with ambari database version other than 'trunk'
You can specify the ambari version number through the **VER** environment variable to initialize initialize the database shema from.

```
docker run -d -P -e VER=<the desired version> --name amabri-dev-psql sequenceiq/ambari-dev-psql
```

## Starting the container with a preset Postgres port number

```
docker run -d -p 7002:5432 --name amabri-dev-psql-trunk sequenceiq/ambari-dev-psql
```

## Connecting to the database from outside the container

```
psql -h $(boot2docker ip) -p <port number the Postgres port 5432 is exposed to> -U ambari -d ambari
```
