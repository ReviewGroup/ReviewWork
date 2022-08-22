

Docker Cgroup Namespace Union FS

docker run -it centos bash 

进入到centos



#### Docker 命令

```
systemctl status docker ： docker 	服务是否启动
Mac launchctl status docker

docker run -it nginx  docker run -it centos bash. 

docker run -d nginx

Docker stop/start containers 

Docker ps -a 

-p 端口映射 -v 挂载磁盘

docker inspect containers

docker exec -it 47a259f869a6 bash 进入运行的容器里 exit

docker cp file.txt 9082a2f925b9:/path 	拷贝文件到容器

docker stats # docker 运行cpu 磁盘信息

docker rmi $(docker images -qf "dangling=true") 清除列出悬挂（dangling）的镜像，显示为<none>
```



#### Dockerfile

```dockerfile
FROM ubuntu/jdk
ENV  port=80  环境变量
ADD bin/httpserver /httpserver 把本地文件添加到镜像 支持URL
COPY <src> <dest> 只支持文件复制
RUN cp /root/ ./ 运行指令
EXPOSE 8080 发布端口
ENTRYPOINT ["/httpserver"] 	启动哪个程序

docker build -f ./dockerfile -t name/httpserver:tag . 当前目录为工作目录
docker push name/httpserver:v1.0
docker run -d name/httpserver:v1.0

docker container logs 7be47500b557  查看容器日志

```

```
lsns -t <type>/net   看namespace

```

Docker save/load 加载或生成tar包



Hotfix 分支提交 在其他分支cherry pick 并提交

git tag -a v1.1 -m""

Git push origin v1.1





#### Company Docker config

##### Consul  

```

docker run --restart always -d -p 8500:8500 -p 8600:8600/udp --name=consul consul agent -dev -client=0.0.0.0
```



##### Docker 内网仓库

```dockerfile
docker buildx build --platform linux/amd64 -t actor-amazon-amd64:v1.0 . 
docker tag actor-amazon-amd64:v1.0 reg.hho-inc.com/cloud-scraper/actor-amazon-amd64:v1.0
docker push reg.hho-inc.com/cloud-scraper/actor-amazon-amd64:v1.0
docker login -u admin -p hhoroot@2022 reg.hho-inc.com
```

##### Docker 公网仓库

```dockerfile
docker login --username=hho-docker@hhodata registry.cn-hangzhou.aliyuncs.com
pwd：DockerHho1234
docker build . -t xxx:1.0
docker images
docker tag 70436d7cf466 registry.cn-hangzhou.aliyuncs.com/cloud-scraper/crawl:1.0
docker push registry.cn-hangzhou.aliyuncs.com/cloud-scraper/crawl:1.0
https://cr.console.aliyun.com/repository/cn-hangzhou/cloud-scraper/actor-docker-controller/details
```



```dockerfile
// todo delete 727

docker login --username=hho-docker@hhodata registry.cn-hangzhou.aliyuncs.com
pwd：DockerHho1234
// 镜像打包
// docker build -f Dockerfile -t imagetest:v1.0 . 
docker buildx build --platform linux/amd64 -f Dockerfile -t competition-image-amd64:v1.1 .  
// 查看打好的镜像
docker images 
docker tag competition-image-amd64:v1.1 registry.cn-hangzhou.aliyuncs.com/cloud-scraper/competitor-image:1.0
docker push registry.cn-hangzhou.aliyuncs.com/cloud-scraper/competitor-image:1.0   

docker run -p 10080:10080 -e searchTerm=毛巾 -e itemId=P227E1606522 -e env=online registry.cn-hangzhou.aliyuncs.com/cloud-scraper/competitor-image:1.0

sudo -u admin curl https://www.amazon.co.jp

```







网关 loadblance   同一鉴权

上云 aws  数据同步
