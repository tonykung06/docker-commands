##Get Started with Docker
###Commands
- `docker log`, to login docker hub
- `docker push <image name>`, to push image to docker hub
- `docker verion`
- `docker info`
- `docker images`
- `docker ps -a`
- `docker tag <image id> <repository>:<your desired tag name, e.g. latest>`
- `docker tag <repository> <new repo name>`, to change the repo name
- `docker run -it --name <desired container name> <repository>:latest /bin/bash`, run <repository>:latest, start cmd and attach console to container console, CTRL+P+Q could exit the container shell
- `docker run -d --name <desired container name> -p 80:8080 <image>`, run the container in detached mode (in background), given a unique name, configured with network port (docker host's port 80 is routed to container's port 8080)
- `docker pull alpine`, to download alphine:latest image from docker hub
- `docker pull ubuntu:14.04`, to download ubuntu:14.04 image from docker hub
- `docker rmi ubuntu:14.04`, to remove ubuntu:14.04 image
- `docker [start | stop | rm] <container name or id>`
- `docker stop $(docker ps -aq)`, to stop all docker containers
- `docker rm $(docker ps -aq)`
- `docker rmi $(docker images -q)`

###Docker Swarm (cluster mode)
- `docker swarm init --advertise-addr 139.162.13.229:2377 --listen-addr 139.162.13.229:2377`, to init a swarm, the ip and port should be able to be reached by all other nodes in the swarm
- `docker swarm join-token manager`, to show command and token to join a new manager into the swarm
- `docker swarm join-token worker`, to show command and token to join a new worker into the swarm
- `docker node ls`
- `docker node promote <node id>`, to promote a worker node to manager role

###Docker Services based on Swarm (native container-aware load balancer => routing mesh)
- `docker service <create | ls | ps | inspect | update | rm>`
- `docker service create --name myservice -p 80:8080 --replicas 5 <image>`
- `docker service ls`
- `docker service ps myservice`
- `docker service inspect myservice`, to see the configs of the service
- `docker service scale myservice=6`, the same as `docker service update --replicas 6 myservice`
- `docker service rm myservice`
- `docker service update --image <v2 image> --update-parallelism 2 --update-delay 10m myservice`, to update app from v1 to v2, 2 nodes at a time and 10m delay in between

###Docker Stacks and Bundles (a stack is an application comprising multiple services, deployed from distributed application bundles)
###Docker compose
- `docker-compose build`, build docker images from docker-compose.yml
- `docker-compose bundle`, make a DAB bundle
- `docker stack deploy <stack DAB name without file suffix, usually the stack name>`
- `docker stack rm <stack name>`

##Docker Deep Dive
- `docker inspect <container name>`
- `docker port <container name>`
- `docker ps`
- `service docker.io status`
- `docker version`
- `docker info`
- `systemctl status docker`
- `systemctl stop docker`
- `systemctl start docker`
- `docker run -it ubuntu /bin/bash`
- `docker run -it centos /bin/bash`
- `netstat -tlp`
- `docker -H <ip>:<port> -d &`
- `docker -H <ip>:<port> -H unix:///var/run/docker.sock -d &`
- `yum check-update`
- `docker ps`
- `docker ps -a`
- `docker start <container id>`
- `docker attach <container id / container name>`
- `docker pull fedora`
- `docker pull -a fedora`
- `docker images fedora`
- CTRL + P + Q to leave a container without killing it
- `docker images`
- `docker run ubuntu /bin/bash -c "echo 'cool content' > /tmp/cool-file"`
- `docker commit <container id> <copy new name>`
- `docker history <the name of the previous new image copy>`
- `docker save -o /tmp/new-testing-image.tar new-testing-image`
- `tar -tf ./new-testing-image.tar`
- `docker load -i <path to the image tar file>`
- `docker run -d ubuntu /bin/bash -c "ping 8.8.8.8 -c 30"`
- `docker ps`
- `docker top <container id>`
- `docker run --cpu-shares=256` //1024 == full cpu
- `docker run memory=1g` 
- `docker inspect <container id>`

https://blog.docker.com/2015/07/new-apt-and-yum-repos/
https://help.github.com/articles/basic-writing-and-formatting-syntax/