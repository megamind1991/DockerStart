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









