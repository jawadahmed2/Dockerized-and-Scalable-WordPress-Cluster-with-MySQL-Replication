Dockerized and Scalable Wordpress Cluster With MySQL Replication
========================

MySQL 8.0 master-slave replication with using Docker. 

## Run

To run this examples you will need to start containers with "docker-compose" 
and after starting setup replication. See commands inside ./build.sh. 

#### Create 2 MySQL containers with master-slave row-based replication 

```bash
./build.sh
```

#### Make changes to master

```bash
docker exec mysql_master sh -c "export MYSQL_PWD=111; mysql -u root mydb -e 'create table code(code int); insert into code values (100), (200)'"
```

#### Read changes from slave

```bash
docker exec mysql_slave sh -c "export MYSQL_PWD=111; mysql -u root mydb -e 'select * from code \G'"
```

## Troubleshooting

#### Check Logs

```bash
docker-compose logs
```

#### Start containers in "normal" mode

> Go through "build.sh" and run command step-by-step.

#### Check running containers

```bash
docker-compose ps
```

#### Clean data dir

```bash
rm -rf ./master/data/*
rm -rf ./slave/data/*
```

#### Run command inside "mysql_master"

```bash
docker exec mysql_master sh -c 'mysql -u root -p111 -e "SHOW MASTER STATUS \G"'
```

#### Run command inside "mysql_slave"

```bash
docker exec mysql_slave sh -c 'mysql -u root -p111 -e "SHOW SLAVE STATUS \G"'
```

#### Enter into "mysql_master"

```bash
docker exec -it mysql_master bash
```

#### Enter into "mysql_slave"

```bash
docker exec -it mysql_slave bash
```
### Restart the container if there is issue

```bash
docker-compose restart
```

### Access The Wordpress Site
- Go to the browser and enter the just
- ``` localhost ```
- The ingnix server will redirect the default localhost 80 to the wordpress 1 site

### Down the Wordpress1 container
- Now for testing, down the wordpress1 container using below command, in this way the wordpress2 will activate and the data is synchronised.
- ```bash
  docker stop wordpress1
  ```
- Now again run the localhost
- And check out the logs so it will show the wordpress2 will be activated
- ```bash
  docker logs wordpress2
  ```

                           ------------------------------------------------------------------------------------------
