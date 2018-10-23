# Install zookeeper

## Docker Image
```bash
$ docker pull zookeeper
```

## Running Zookeeper
### Single Node
- Running zookeeper container with command:
```bash
$ docker run --name zookeeper01 -d -p 2181:2181 zookeeper
```
default port is 2181.

- Check zookeeper logs:
```bash
docker logs -f zookeeper01
```
- Go into zookeeper container:
```bash
docker exec -it zookeeper01 /bin/bash
```

- Running zkCli.sh
```bash
docker run -it --rm --link zookeeper01:zookeeper zookeeper zkCli.sh -server zookeeper
```

### Zookeeper cluster
docker-compose.yml
- ZOO_MY_ID: Zookeeper instance ID
- ZOO_SERVERS: Zookeeper cluster server list

start cluster:
```bash
$ docker-compose -f docker-compose.yml up -d
```
running client:
```bash
docker run -it --rm --link zookeeper01:zookeeper --net docker-zookeeper_default zookeeper zkCli.sh -server zookeeper
```
stop cluster:
```bash
$ docker-compose -f docker-compose.yml down
```

## Reference
https://hub.docker.com/_/zookeeper/
