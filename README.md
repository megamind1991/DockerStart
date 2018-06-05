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

容器中启动新的进程
 
