# grafana-build-custom-docker-image

# 🚀 Build and run a Grafana Docker image with pre-installed plugins 🚀

https://github.com/coding-to-music/grafana-build-custom-docker-image

From / By https://grafana.com/docs/grafana/latest/setup-grafana/installation/docker/

## Environment variables:

```java

```

## GitHub

```java
git init
git add .
git remote remove origin
git commit -m "first commit"
git branch -M main
git remote add origin git@github.com:coding-to-music/grafana-build-custom-docker-image.git
git push -u origin main
```

## docker-compose up

```java
docker-compose up
```

Output:

```java

```

## docker-compose down

```
docker-compose down
```

Output

```java

```

## checking ports and who uses them

https://linuxhandbook.com/check-open-ports-linux/

```
sudo netstat -nlp
```

```java
sudo lsof -i

sudo lsof -i -P -n

sudo lsof -i -P -n | grep LISTEN

nc -z -v <IP-ADDRESS> 1-65535 2>&1 | grep -v 'Connection refused'

sudo netstat -lptu

sudo netstat -tulpn

nc -z -v <IP-ADDRESS> 1-65535 2>&1 | grep -v 'Connection refused'

```

## Docker commands

```
docker-compose up

docker-compose down

docker-compose up --remove-orphans

docker-compose restart grafana

docker ps

docker volume ls
```

# Build and run a Docker image with pre-installed plugins

https://grafana.com/docs/grafana/latest/setup-grafana/installation/docker/

You can build your own customized image that includes plugins. This saves time if you are creating multiple images and you want them all to have the same plugins installed on build.

In the Grafana GitHub repository there is a folder called packaging/docker/custom/, which includes two Dockerfiles, Dockerfile and ubuntu.Dockerfile, that can be used to build a custom Grafana image. It accepts `GRAFANA_VERSION, GF_INSTALL_PLUGINS, and GF_INSTALL_IMAGE_RENDERER_PLUGIN` as build arguments.

## Build with pre-installed plugins

If you need to specify the version of a plugin, you can add it to the `GF_INSTALL_PLUGINS` build argument. Otherwise, the latest will be assumed. For example: `--build-arg "GF_INSTALL_PLUGINS=grafana-clock-panel 1.0.1,grafana-simple-json-datasource 1.3.5"`

Example of how to build and run:

cd packaging/docker/custom

```java
docker build \
  --build-arg "GRAFANA_VERSION=latest" \
  --build-arg "GF_INSTALL_PLUGINS=grafana-clock-panel,grafana-simple-json-datasource" \
  -t grafana-custom -f Dockerfile .
```

```
docker run -d -p 3000:3000 --name=grafana grafana-custom
```
