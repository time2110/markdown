Docker使用
```
Docker容器使用
获取镜像：docker pull ubuntu
启动容器：docker run -it ubuntu /bin/bash
查看容器：docker ps -a
启动已停止容器：docker start <容器 ID> 
后台运行：docker run -itd --name ubuntu-test ubuntu /bin/bash
映射地址：docker run -itd -v /script:/script --name script python:3.9.6 /bin/bash
停止容器：docker stop <容器 ID>
进入容器：docker exec -it <容器 ID> /bin/bash
导出容器：docker export <容器 ID> > ubuntu.tar
导入容器：cat docker/ubuntu.tar | docker import - test/ubuntu:v1
		  docker import http://example.com/exampleimage.tgz example/imagerepo
删除容器：docker rm -f <容器 ID>
```
```
Docker镜像使用
查看镜像列表：docker images
获取镜像：docker pull ubuntu
查找镜像：docker search httpd
删除镜像：docker rmi <镜像 名称>
更新镜像：从已创建的容器中更新镜像，并且提交这个镜像
提交镜像：docker commit -m="描述信息" -a="作者" <容器 ID>
runoob/ubuntu:v2
设置镜像标签：docker tag <容器 ID> runoob/centos:dev
```
```
Docker容器连接
网络端口映射
docker run -d -P training/webapp python app.py
docker run -d -p 5000:5000 training/webapp python app.py
// 默认都是绑定 tcp 端口，如果要绑定 UDP 端口，可以在端口后面加上 /udp
docker run -d -p 5000:5000/udp training/webapp python app.py

-P :是容器内部端口随机映射到主机的端口。
-p : 是容器内部端口绑定到指定的主机端口。
```
```
Docker容器互联
新建网络：docker network create -d bridge test-net
连接容器：运行多个容器并连接到新的网络
docker run -itd --name test1 --network test-net ubuntu /bin/bash
docker run -itd --name test2 --network test-net ubuntu /bin/bash
配置DNS：
 /etc/docker/daemon.json 文件中增加以下内容来设置全部容器的 DNS：
{   "dns" : [     "114.114.114.114",     "8.8.8.8"   ]  }
在指定的容器设置 DNS：
docker run -it --rm -h host_ubuntu  --dns=114.114.114.114 --dns-search=test.com ubuntu

apt-get update
apt install iputils-ping
// ping test1 test2
```

