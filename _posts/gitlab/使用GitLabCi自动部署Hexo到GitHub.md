---
title: 使用GitLab Ci 自动部署Hexo到GitHub
date: 2020-07-18 22:37:22
tags: [gitlab,树莓派]
---
## 废话
使用GitLab 自动部署到github 省去了在自己电脑上装node的一堆潜在问题，只管写想发就发，户体验极度攀升
为啥不直接发布到gitlab pages呢？我的gitlab是部署在树莓派里的，博客发布到gitlab的pages指不定哪天就凉了,还有xss的问题，所以还是发布到github吧

### 在gitlab中创建一个私有仓库

### 向项目目录下添加私钥

###
将公共ssh密钥添加到您的github
将.gitlab-ci.yml添加到您的项目

###
private_key是私钥
,hexo-generator-searchdb,用于生成网站搜索功能
,hexo-abbrlink --save这个是生成唯一永久文章链接用的,这些都需要相应的在hexo中配置才能生效
推送您的更改并查看结果:)
 
## .gitlab-ci.yml

```
image: node:lts-alpine
cache:
  paths:
    - node_modules/

before_script:
  - npm config set registry https://registry.npm.taobao.org/
  - npm install hexo-cli -g
  - npm install hexo-generator-searchdb --save
  - npm install hexo-abbrlink --save
  - npm install hexo-deployer-git --save
  - npm install
  - sed -i 's/dl-cdn.alpinelinux.org/mirrors.aliyun.com/g' /etc/apk/repositories
  - apk --update add openssh-client
  - apk --update add git
  - eval $(ssh-agent -s)
  - chmod 700 private_key
  - ssh-add private_key
  - git config --global user.email "xxxx@xx.com"
  - git config --global user.name "xxxx"
  - echo StrictHostKeyChecking no >> /etc/ssh/ssh_config

pages:
  script:
    - hexo generate --deploy
  artifacts:
    expire_in: 1 day
    paths:
      - public
  only:
    - master
```
