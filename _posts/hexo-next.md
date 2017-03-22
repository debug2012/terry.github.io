---
title: 使用 github pages，hexo，next搭建博客系统
date: 2017-03-21 23:01:35
tags: hexo next
---
## 配置github

- 注册github，假设账号为demo
- 创建博客项目，demo.github.io，注意demo是账号名，这里一定要跟账号保持一致，否则不能访问到项目 
- 配置ssh-key，不用每次deploy的时候都要输入账号密码
```
ssh-keygen -t rsa -C '你github的邮箱地址'
```
拷贝公钥文件~/.ssh/id_rsa.pub到https://github.com/settings/keys

## 全局安装hexo

```
npm install hexo -g
```
### 初始化博客项目
```
hexo init myblog
```

## 安装next主题

```
cd myblog
git clone https://github.com/iissnan/hexo-theme-next themes/next
```

### 配置next主题
```
cd themes/next
vi _config.yaml
```
配置scheme,最好挨个设置一下看看效果
```
#scheme: Muse #默认
scheme: Mist
#scheme: Pisces
```

使用next 自带的disqus配置来开启评论功能
```
disqus_shortname: debug2012 #debug2012是笔者在[disqus](https://www.disqus.com)上注册一个shortname
```
更多next主题的配置，可以参考 http://theme-next.iissnan.com/getting-started.html
### 修改myblog配置
```
language: zh-Hans #中文
timezone: Asia/Shanghai
theme: next

deploy:
  type: git
  #复制上面创建的项目的ssh地址
  repo: git@github.com:demo/demo.github.io.git
  branch: master #提交master分支上
```

> ## 使用hexo

### 新建一篇blog
```
hexo new "hello world"
```
More info: [Writing](https://hexo.io/docs/writing.html)

### 启动本地server预览
```
hexo server
或者
hexo s # hexo s --debug debug模式，修改博客内容可以重新加载
```
More info: [Server](https://hexo.io/docs/server.html)

### 生成静态文件

```
hexo g # 或 hexo generate
```
More info: [Generating](https://hexo.io/docs/generating.html)

## 发布hexo

```
hexo deploy
```
如果出现'ERROR Deployer not found: git'错误提示，需要安装deploy模块
```
npm install hexo-deploy
```
More info: [Deployment](https://hexo.io/docs/deployment.html)

## 访问博客

https://demo.github.io


