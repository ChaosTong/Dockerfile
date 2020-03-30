## Usage

``` shell
docker ps -a # list container
docker images # list images

docker rm <id> # rm container
docker rmi <id> # rm image

docker build -f /path/to/a/Dockerfile . # build image with specific Dockerfile path
docker build -t name:tag . # build image with Dockerfile current directory use -t name:tag e.g. alpine_base:v1

docker run -it alpine_base:v1 /bin/zsh # run with name through shell

```