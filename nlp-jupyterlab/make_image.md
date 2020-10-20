# Install Docker
sudo yum remove docker \
                  docker-client \
                  docker-client-latest \
                  docker-common \
                  docker-latest \
                  docker-latest-logrotate \
                  docker-logrotate \
                  docker-engine
阿里云Docker Yum源
sudo yum install -y yum-utils device-mapper-persistent-data lvm2
sudo yum-config-manager --add-repo http://mirrors.aliyun.com/docker-ce/linux/centos/docker-ce.repo
sudo yum makecache fast
sudo yum -y install docker-ce

# Docker basic config
sudo groupadd docker
sudo gpasswd -a s docker #s表示当前使用的用户
sudo systemctl restart docker

su root
su s
docker ps -a

- 开机启动docker
systemctl enable docker.service

- 常用命令
docker version
docker images
docker ps -a
docker rm xxx
docker rmi xxx
docker stop xxx
docker run -it --restart=always
docker exec -it id123 /bin/bash

systemctl enable docker
systemctl status docker
service docker start
service docker restart
service docker stop

# 安装 Compose
curl -L https://github.com/docker/compose/releases/download/1.3.1/docker-compose-`uname -s`-`uname -m` > /usr/local/bin/docker-compose
chmod +x /usr/local/bin/docker-compose

# Test image
docker run -rm -p 8888:8888 jupyter/scipy-notebook

# Make image
name: huavarlab/nlp-jupyterlab:0.1.0
CMD: docker build -t {name} -f Dockerfile .

# image save and load
docker save -o nginx.tar nginx:latest

docker load -i nginx.tar


## from Container create Image
//查看所有的容器
docker container ls -a
 
//8a5d6fd69453是原容器id，gmk/centos-vim是新image的REPOSITORY
docker commit 8a5d6fd69453 gmk/centos-vim
 
//查看新镜像
docker image ls


## offline install pip 

pip download docker-compose

pip install --no-index --find-links=file:/offline_package_dir docker-compose

