# tech201_Docker

Firstly you can install docker from dockers website, after this has been downloaded use the following commands and then then in order to check this is working type version and run hello-world.
https://docs.docker.com/desktop/install/windows-install/
```
"Docker Desktop Installer.exe"
Start-Process 'Docker Desktop Installer.exe' -Wait install
start /w "" "Docker Desktop Installer.exe" install

docker --version
docker run hello-world
```
## Login

Login to docker 

```
docker login
```
## Linking Repositories

You can use the following commands to build and then push an image to your docker repositories, change the dockeraccount, repo and tag to the one listed, which you can find with the first command.

```
docker images
docker ps
docker build -t dockeraccount/repo:tag
docker push dockeraccount/repo:tag

```

You can tag an image with the following , as it needs a tag to be pushed , using your own reponame and dockeraccount and the changes can be commmited with docker commit.

```
docker tag dockeraccount/repo
docker commit id dockeraccount/repo
docker push dockeraccount/repo
```

## Running your Image

The image can be run to display its content on a local server with the following, with your own dockeraccount , repo and tag. the 80:80 can be changed to your prefered port while keeping the second 80 as the port of the image , such as 100:80 .

```
ducker run -d -p 80:80 dockeracount/repo:tag