---
title: docker配置
date: 2020-07-25 16:01:22
tags: [docker,树莓派]
---
## linux安装docker

### 官方安装文档
>https://docs.docker.com/engine/install/debian/
这里用的是脚本一键安装的方案,使用阿里云镜像加速

`curl -fsSL https://get.docker.com -o get-docker.sh`

`sudo sh get-docker.sh --mirror Aliyun`

### use Docker as a non-root user

`sudo usermod -aG docker your-user`

### docker配置镜像加速器,阿里云的需要登录账号获取

```
sudo mkdir -p /etc/docker
sudo tee /etc/docker/daemon.json <<-'EOF'
{
  "registry-mirrors": [
	"https://hub-mirror.c.163.com",
    "https://reg-mirror.qiniu.com"]
}
EOF
sudo systemctl daemon-reload
sudo systemctl restart docker
```

## 安装 docker-compose
linuxserver官方地址
>https://hub.docker.com/r/linuxserver/docker-compose

```
sudo curl -L --fail https://raw.githubusercontent.com/linuxserver/docker-docker-compose/master/run.sh -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose
```

## docker-compose 开机启动

### 编写debian系开机启动脚本

```
#!/bin/bash
### BEGIN INIT INFO
# Default-Start:  2 3 4 5
# Default-Stop: 0 1 6
### END INIT INFO

cd /home/pi/docker/

docker-compose -f docker-compose.yml up -d
```
上传启动脚本到 /etc/init.d 目录下
`cd /etc/init.d`
`chmod 755 dockerup`

#设置开机自启
`sudo update-rc.d dockerup defaults`

#删除开机自启
`sudo update-rc.d -f dockerup remove`

