# DockerStart
DockerStart

简单容器

docker run ubuntu echo 'hello world'  一次启动一次执行容器

启动交互式容器（进入容器操作）

docker run -i -t IMAGE /bin/bash  i打开标准输入 t 终端

docker ps -a -l                   a是全部 l是最后一个 查看所有容器

docker inspect 【容器ID 或者 名字 】 查看容器详情

docker run --name=XXXX -i -t ubuntu /bin/bash 建立一个自定义名字的容器

docker start -i containerName 重新启动容器

docker rm containerName 删除停止了的容器 不能停止正在运的容器



=======================================================================================================
长期的 守护式容器 

docker run -i -t IMAGE /bin/bash 和 Ctrl Q Ctrl P 的组合 可以保证后台运行

docker attach containerID/Name 重新进入容器的命令

docker run -d ubuntu /bin/sh -c "while true; do echo hello world; sleep 1; done"  -d意思是后台运行 运行结束后就消灭 容器

docker logs -f -t --tail         f一直跟踪 t时间戳 tail末尾的

docker top 容器民  容器的进程状况

docker exec  -d -i -t  ContainerName /bin/bash [arg]           容器中启动新的进程
 
docker stop Cname  / docker kill Cname 停止守护容器

============================================================================================================

容器中进行部署

-P -p 大P 对外开放所有端口  小p对外开放指定端口

docker run -p 80 --name web -i -t ubuntu /bin/bash

docker run -p 8080:80 --name web -i -t ubuntu /bin/bash

docker run -p 80 --name web -i -t ubuntu /bin/bash

docker run -p 0.0.0.8080:80 --name web -i -t ubuntu /bin/bash

docker ps 中可以看到 容器端口 映射的主机端口号

docker port web 也可以看都端口的映射状况

docker top web 可以看到 web容器中 运行的nginx的运行进程

docker inspect web 命令 可以看到容器内的ip地址

docker exec web nginx 命令 启动web容器中的nginx

重启容器之后 端口是会改变的 请注意。。。

============================================================================================================

镜像的学习 

docker info 查看docker的驱动以及存储位置 存贮位置里面有很多镜像

列出镜像

docker images -a -f -no-trunc -q RepositoryAddress 

docker images 返回已经在docker中安装的镜像

docker inspect imgName 查看镜像的详细命令 及支持容器有支持镜像的详细查看

docker rmi imgName  删除镜像

查找镜像 从仓库中

docker search  ubuntu

docker pull -a imgName：tag   拉去镜像

加速拉去镜像 修改 /etc/default/docker 添加 DOCKER_OPT = "--registry-mirror=http://国内的镜像地址"

docker push imgName：tag     推送镜像

自己的镜像的 创建

docker commit 通过容器创建镜像 docker build 通过dockerFile构建

docker commit --auther --message -p containerName imgName

docker build -t-"文件路径"

==========================================================================================================

Docker C/S 模式

RemoteAPI

-u sockt访问

service docker stop

service docker start

service docker restart

Docker守护线程的 启动选项

docker的启动配置文件 etc/default/docker

-H 进行远程链接 一台dockerClient 一台dockerService

===============================================================================================================

Docker 容器的网络基础

容器会有一个虚拟网卡 与docker 进行桥接 docker0 虚拟网桥

docker容器 互联

-icc 允许互相链接

docker run it --name cct3 --link=containName：webtest imgname

拒绝容器访问

--icc =false

循序特地链接 

--icc = false  --iptables=true 
--link
主要是link命令 的别名很重要

===================================================================================================================

docker 数据卷

docker run -it -v ~/datavolume:/data ubuntu /bin/bash               添加数据卷

docker run -it -v ~/datavolume:/data:ro --name dvt1 ubuntu /bin/bash     添加访问权限

dockerFile 中创建数据卷 效果完全不一样

docker run --volumes-from containName 创建一个docker数据卷容器  这已经不是 像上面的数据卷了  实现docker容器间的数据 共享

备份 与 还原

======================================================================================================================

跨主机 容器链接  网桥方式



============================================================================

与swarm一起使用 搭建集群

docker swarm：集群管理，子命令有 init, join,join-token, leave, update
docker node：节点管理，子命令有 demote, inspect,ls, promote, rm, ps, update
docker service：服务管理，子命令有 create, inspect, ps, ls ,rm , scale, update
docker stack/deploy：试验特性，用于多应用部署，等正式版加进来再说。


swarmkit的引入，在docker中引入了三个子命令：

docker swarm——swarm集群搭建
docker service——服务管理
docker node——集群节点管理

docker swarm 子命令
查看子命令 vagrant@test1:~$ docker swarm –help

  init        初始化swarm集群
  join        将当前节点加入到集群中
  join-token  管理加入token
  update      动态更新swarm配置
  leave       当前节点主动退出集群(仅限worker节点)

docker service 子命令
查看子命令 vagrant@test1:~$ docker service –help

create      创建服务
inspect     显示服务详情
ps          列出服务中的容器
ls          列出所有服务及简介
rm          删除服务
scale       调整服务的副本数
update      动态更新服务配置

docker node 子命令
查看子命令 vagrant@test1:~$ docker node –help

demote      管理节点为指定子节点降权
inspect     显示节点详情
ls          列出集群中的节点
promote     管理节点为指定子节点提权
rm          删除一个节点
ps          列出指定子节点中running的容器
update      动态更新节点配置















