```
docker pull splunk/splunk:latest
```

```
sudo docker run -d -p 8000:8000 -e "SPLUNK_START_ARGS=--accept-license" -e "SPLUNK_PASSWORD=mypassw0rd" --restart unless-stopped -it --name spl1 splunk/splunk:latest
```

```
docker ps
```

| Command             | Description                             |
| ------------------- | --------------------------------------- |
| `docker ps`         | List running containers                 |
| `docker ps -a`      | List all containers (including stopped) |
| `docker images`     | List downloaded images                  |
| `docker volume ls`  | List volumes                            |
| `docker network ls` | List networks                           |
| `docker system df`  | Show disk usage of Docker resources     |
