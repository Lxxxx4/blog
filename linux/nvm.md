# nvm安装

使用git安装
- cd ~/ - -切到主目录
- git clone https://github.com/creationix/nvm.git .nvm - -克隆代码到文件夹 .nvm
- cd ~/.nvm - -进入nvm代码目录
- git checkout v0.33.11 - -切换到v0.33.11版本
- . nvm.sh - -执行命令


> 查看远程版本
nvm ls-remote

> 安装版本
nvm install 10.9.0

> 切换版本
nvm use 10.9.0

> 查看所有版本
nvm ls

> 设置国内镜像
export NVM_NODEJS_ORG_MIRROR=https://npm.taobao.org/mirrors/node
