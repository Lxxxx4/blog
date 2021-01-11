#### 基础指令

```
# apt-get

sudo apt-get update # 更新软件列表

sudo apt-get upgrade -y # 对比各软件版本并更新

sudo apt-get install nodejs -y # 安装nodejs

sudo apt-get install npm -y # 安装npm

sudo npm install n -g # 安装nodejs版本管理器

n latest # 更新nodejs至最新版本，可自行选择，更新完成记得重新连接服务器输入 node -v 检查是否更新成功

sudo npm install pm2 -g # 安装pm2，node进程管理工具，这里主要用于持久化运行和监控nestjs服务器

# yum
#yum check-update
#yum remove 软件包名
#yum install 软件包名
#yum update 软件包名
yum命令常见使用方法
yum -y install 包名（支持*） ：自动选择y，全自动
yum install 包名（支持*） ：手动选择y or n
yum remove 包名（不支持*）
rpm -ivh 包名（支持*）：安装rpm包
rpm -e 包名（不支持*）：卸载rpm包

#安装
sudo apt-get install nginx -y # 安装nginx服务器
sudo yum -y install nginx
service nginx start # 启动nginx服务器
#安装MySQL。
sudo yum list installed mysql* 查看是否安装了mysql
sudo yum -y install mysql
sudo yum install mysql-server
#先执行
sudo rpm -Uvh http://dev.mysql.com/get/mysql-community-release-el7-5.noarch.rpm 
#继续执行 yum install mysql-server 
sudo yum install mysql-devel

service mysqld start      --启动mysql
service mysqld stop       --关闭mysql·
lsof -i:3306              --数据库端口是否开启
```

