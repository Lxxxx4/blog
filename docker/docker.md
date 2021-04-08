# docker

## ubuntu下安装

```js
// 更新软件包索引
sudo apt update
// 安装必要的依赖软件
sudo apt install apt-transport-https ca-certificates curl gnupg-agent software-properties-common
// 使用下面的 curl 导入源仓库的 GPG key
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
// 将 Docker APT 软件源添加到你的系统
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
// 想要安装 Docker 最新版本
sudo apt update
sudo apt install docker-ce docker-ce-cli containerd.io
// 一旦安装完成，Docker 服务将会自动启动。你可以输入下面的命令，验证它：
sudo systemctl status docker
// 如果你想阻止 Docker 自动更新，锁住它的版本：
sudo apt-mark hold docker-ce
// 默认情况下，只有 root 或者 有 sudo 权限的用户可以执行 Docker 命令。
// 想要以非 root 用户执行 Docker 命令，你需要将你的用户添加到 Docker 用户组，该用户组在 Docker CE 软件包安装过程中被创建。想要这么做，输入：
// $USER是一个环境变量，代表当前用户名。
sudo usermod -aG docker $USER
// 如果本地没有该镜像，这个命令将会下载测试镜像，在容器中运行它，打印出 “Hello from Docker”，
docker container run hello-world

```

## 创建一个docker镜像并运行
### 编写Dockerfile
```js
// 基于FROM的镜像定制你的镜像
FROM node:12-alpine
// 用于执行后面跟着的命令行命令
RUN apk add --no-cache python g++ make
// 指定工作目录。
WORKDIR /app
// 复制指令，从上下文目录中复制文件或者目录到容器里指定路径。
COPY . .
RUN yarn install --production
// 类似于 RUN 指令，用于运行程序，但二者运行的时间点不同:
// CMD 在docker run 时运行。
// RUN 是在 docker build。
CMD ["node", "src/index.js"]
```
### 创建docker镜像
```js
// 使用当前目录的Dockerfile创建镜像， -t 后面带镜像的名字
docker build -t getting-started .
```

### 运行docker镜像
```js
// -d 表示后台运行容器，并返回容器ID -p表示端口号
docker run -dp 3000:3000 getting-started
//  -v 绑定一个卷
docker run -dp 3000:3000 -v todo-db:/etc/todos getting-started
```
### docker指令
```js
// 列出容器
docker ps
// 停止一个运行中的容器
docker stop
//移除一个容器
docker rm 
// 删除所有容器
docker stop $(docker ps -q) & docker rm $(docker ps -aq)
// 列出镜像
docker images
// 删除一个镜像
Docker rmi <image-name>:tag-name
// 删除所有镜像
docker rmi $(docker images -q) -f
// 给镜像添加标签
docker tag old_container_name  new_container_name
// 登录docker pub
docker login -u YOUR-USER-NAME
// 推送本地镜像
docker push YOUR-USER-NAME/getting-started
// 在运行的容器中执行命令，使用exit退出   -d :分离模式: 在后台运行 -i :即使没有附加也保持STDIN 打开 -t :分配一个伪终端 
docker exec 
// 创建一个卷积
docker volume create <volumn-name>
// 查看所有容器卷积
docker volume ls
//  查看指定容器卷详情信息
docker volume inspect <volumn-name>
// 获取容器的日志， -f : 跟踪日志输出
docker logs -f <container-id>
```
