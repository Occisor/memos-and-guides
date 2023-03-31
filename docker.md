# docker-commands

### Копирование файла с контейнера на хост и наоборот
Можно выполнять как на запущенном контейнере, так и остановленном.  
Скопировать файл `wg-quick` из контейнера `wg-3p.wireguard_cli.1` в директорию на `/home/user/` на хосте.
```
docker cp wg-3p.wireguard_cli.1:/usr/bin/wg-quick /home/user/
```
Скопировать файл `wg-quick` из диретории хоста `/home/user/` в контейнера `wg-3p.wireguard_cli.1`.
```
docker cp /home/user/ wg-3p.wireguard_cli.1:/usr/bin/wg-quick
```
---
### Docker Compose allows us to execute commands inside a Docker container.
During the container startup, we can set any command via the command instruction.
Let's take a look at a `docker-compose.yml`, which runs a simple command inside a container:
```
version: "3"
services:
 server:
   image: alpine
   command: sh -c "echo "test""
```
In the above `docker-compose.yml` file, we are executing a single echo command inside the alpine Docker image.

---
