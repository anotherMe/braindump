
# Running Oracle inside a docker container

Below you'll find instructions to build and run an Oracle XE 21 inside a docker container.

## Build

```bash
git clone https://github.com/oracle/docker-images
cd docker-images/OracleDatabase/SingleInstance/dockerfiles/21.3.0
docker build -t oracle/database:21.3.0-xe -f Dockerfile.xe .
```

## Run

```bash
docker run --name mighty_walrus -p 41521:1521 -p 41500:5500 -e ENABLE_ARCHIVELOG=true oracle/database:21.3.0-xe
```

For further container customization, please refere to the [README](https://github.com/oracle/docker-images/tree/main/OracleDatabase/SingleInstance)


### Password 

If an admin password where not provided during container creation, you have to set one mandatorily. 

You do that when the container is running:

```bash
cd docker-images/OracleDatabase/SingleInstance/dockerfiles/21.3.0
docker exec <container name> ./setPassword.sh <your password>
```

Oracle recommends that the password entered should be at least 8 characters in length, contain at least 1 uppercase character, 1 lower case character and 1 digit [0-9].
 

## Connect

**Note**: The ORACLE_SID for Express Edition is always **XE** and cannot be changed, hence there is no ORACLE_SID parameter provided for the XE build.

