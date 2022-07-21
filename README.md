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

docker build \
  --build-arg "GRAFANA_VERSION=latest" \
  --build-arg "GF_INSTALL_PLUGINS=snuids-radar-panel 1.4.4, grafana-piechart-panel 1.4.0, grafana-worldmap-panel 0.2.1, vonage-status-panel 1.0.9, natel-discrete-panel, briangann-gauge-panel, jdbranham-diagram-panel, grafana-simple-json-datasource" \
  -t grafana-custom -f Dockerfile .

```

```
docker run -d -p 3000:3000 --name=grafana grafana-custom

docker run -d -p 3000:3000 --name=grafana-custom grafana-custom
```

# Publishing your Custom Docker Image on Docker Hub

https://www.howtoforge.com/tutorial/building-and-publishing-custom-docker-images/

Your next option is to publish the created Docker image on the Docker Hub Repository. To do so, you will need to create an account on the Docker Hub signup webpage where you will provide a name, password, and email address for your account. I should also point out that the Docker Hub service is free for public docker images. Once you have created your account, you can push the image that you have previously created, to make it available for others to use.

To do so, you will need the ID and the TAG of your “my-docker-whale” image.

Run again the "docker images" command and note the ID and the TAG of your Docker image e.g. a69f3f5e1a31.

Now, with the following command, we will prepare our Docker Image for its journey to the outside world (the accountname part of the command is your account name on the Docker Hube profile page):

```java
docker tag a69f3f5e1a31 accountname/my-docker-whale:latest

docker tag 2b4ebf47e80b thomasconnors/grafana-custom:latest
```

Run the "docker images" command and verify your newly tagged image.

Next, use the "docker login" command to log into the Docker Hub from the command line.

The format for the login command is:

```java
docker login --username=yourhubusername --email=youremail@provider.com
```

When prompted, enter your password and press enter.

Now you can push your image to the newly created repository:

```java
docker push accountname/my-docker-whale

docker push thomasconnors/grafana-custom
```

The above command can take a while to complete depending on your connection's upload bandwidth as it uploads something like 180ΜΒ of data (in our example). Once it has completed, you can go to your profile on Docker Hub and check out your new image.

## Downloading your Custom Image

If you want to pull your image from your Docker Hub repository you will need to first delete the original image from your local machine because Docker would refuse to pull from the hub as the local and the remote images are identical.

As you remember from the previous part, to remove a docker image, you must run the "docker rmi" command. You can use an ID or the name to remove an image:

```java
docker rmi -f a69f3f5e1a31
```

Now that the image is deleted you can pull and load the image from your repository using the "docker run" command by including your account name from Docker Hub.

```java
docker run accountname/my-docker-whale
```

Since we previously deleted the image and it was no longer available on our local system, Docker will download it and store it in the designated location.
