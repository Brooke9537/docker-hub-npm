# docker镜像加速站 

## 介绍 
**本项目是基于cloudflare worker运行的docker镜像加速站**

**Docker镜像加速站是一种通过配置国内或国际的镜像加速器，来提高从Docker Hub等官方仓库拉取镜像的速度和稳定性的服务。**

## 项目地址
### ![GitHub Repo stars](https://img.shields.io/github/stars/520svip/docker-hub-npm.svg) GitHub：[https://github.com/520svip/docker-hub-npm](https://github.com/520svip/docker-hub-npm)
### ![Gitee Repo stars](https://gitee.com/svip520/docker-hub-npm/badge/star.svg) Gitee：[https://gitee.com/svip520/docker-hub-npm](https://gitee.com/svip520/docker-hub-npm)

## 演示网站
### [https://docker.brooke.fun](https://docker.brooke.fun)


## 部署教程
#### 1、下载定义的依赖包：
```
npm install
```
#### 2、修改配置文件 src/index.js ：
##### 调整workers_url、workers_host为自己CloudFlare的域名
```
let workers_url = 'https://docker.1panel.dev';
const workers_host = 'docker.1panel.dev'
```
#### 3、修改配置文件 wrangler.toml ：
##### 调整routers部分为自己CloudFlare的域名（建议留空，后续去CF控制台手动配置）
```
routes = [
  { pattern = "docker.1panel.dev/*", zone_name = "1panel.dev" },
  { pattern = "hub.1panel.dev/*", zone_name = "1panel.dev" },
  { pattern = "quay.1panel.dev/*", zone_name = "1panel.dev" },
  { pattern = "gcr.1panel.dev/*", zone_name = "1panel.dev" },
  { pattern = "k8s-gcr.1panel.dev/*", zone_name = "1panel.dev" },
  { pattern = "k8s.1panel.dev/*", zone_name = "1panel.dev" },
  { pattern = "ghcr.1panel.dev/*", zone_name = "1panel.dev" },
  { pattern = "cloudsmith.1panel.dev/*", zone_name = "1panel.dev" },
  { pattern = "nvcr.1panel.dev/*", zone_name = "1panel.dev" },
]
```
#### 4、预览和测试应用程序：
```
npx wrangler dev
```
#### 5、部署应用程序置Cloudflare Workers：
```
npx wrangler deploy
```

## 使用方法①
#### 原拉取镜像命令：
```
docker pull library/alpine:latest
```
#### 加速拉取镜像命令：
```
docker pull docker.brooke.fun/library/alpine:latest
```

## 使用方法②
#### 一键设置镜像加速：修改文件 /etc/docker/daemon.json（如果不存在则创建）
```
nano /etc/docker/daemon.json
```
#### 修改JSON文件 更改为以下内容 然后保存
```
{
  "registry-mirrors": ["https://docker.brooke.fun"]
}
```
重载systemd管理守护进程配置文件
```
sudo systemctl daemon-reload
```
重启 Docker 服务
```
sudo systemctl restart docker
```

## 使用方法③
#### 为了加速镜像拉取，使用以下命令设置registry mirror：
```
sudo tee /etc/docker/daemon.json <<EOF
{
    "registry-mirrors": ["https://docker.brooke.fun"]
}
EOF
```
重载systemd管理守护进程配置文件
```
sudo systemctl daemon-reload
```
重启 Docker 服务
```
sudo systemctl restart docker
```

## 镜像加速服务使用协议
**用户在使用本程序时，需遵守当地法律法规，任何因非法使用本程序而导致的法律责任，由用户自行承担，与本程序开发者无关。**
- 请用户在使用本程序时，遵守法律法规，不得用于任何非法目的，否则后果自负。
- 使用者在使用本程序时，需自行承担风险，本程序开发者不对任何因使用本程序而导致的任何直接或间接损失承担责任。
- 使用者在使用本程序时，需自行承担风险，并同意不会因使用本程序而向开发者提出任何索赔要求。
- 使用本程序即视为同意本免责声明的所有条款。如果使用者不同意本免责声明的任何条款，请立即停止使用本程序。
