# Xray + Argo for PaaS

为容器平台而生

* * *

# 目录

- [项目特点](README.md#项目特点)
- [部署](README.md#部署)
- [鸣谢下列作者的文章和项目](README.md#鸣谢下列作者的文章和项目)
- [免责声明](README.md#免责声明)

* * *

## 项目特点:
* 本项目用于在 PaaS 平台上部署 Xray，采用的方案为 Argo + Xray + WebSocket + TLS
* 使用 CloudFlare 的 Argo 隧道，直接优选 + 隧道，CDN 不用再做 workers
* Xray 核心文件作了“特殊处理”，每个项目都不同，大大降低被封和连坐风险
* 回流分流，同时支持 Xray 4 种主流协议: vless /  vmess / trojan / shadowsocks
* vmess 和 vless 的 uuid，trojan 和 shadowsocks 的 password，各协议的 ws 路径既可以自定义，又或者使用默认值
* 集成哪吒探针，可以自由选择是否安装
* 没有使用伪装网页，减少资源占用，因为只会给平台封，几乎不会给 GFW 封
* 节点信息以`Clash`和`小火箭链接`方式输出

## 部署:
* 镜像 `fscarmen/argo-xary:latest` (注:这里 xray 不是拼错，是改一下关键词而已)

* PaaS 平台用到的变量
  | 变量名        | 是否必须 | 默认值 | 备注 |
  | ------------ | ------ | ------ | ------ |
  | UUID         | 否 | de04add9-5c68-8bab-950c-08cd5320df18 | 可在线生成 https://www.zxgj.cn/g/uuid |
  | WSPATH       | 否 | argo | 勿以 / 开头，各协议路径为 `/WSPATH-协议`，如 `/argo-vless`,`/argo-vmess`,`/argo-trojan`,`/argo-shadowsocks` |
  | NEZHA_SERVER | 否 |        | 哪吒探针服务端的 IP 或域名 |
  | NEZHA_PORT   | 否 |        | 哪吒探针服务端的端口 |
  | NEZHA_KEY    | 否 |        | 哪吒探针客户端专用 Key |
  | PORT         | 否 | 8080   | 入站端口，需要在平台里转发(route)该端口 |

* GitHub Actions 用到的变量

  | 变量名 | 备注 |
  | --------------- | -------------- |
  | DOCKER_USERNAME | Dockerhub 用户名|
  | DOCKER_PASSWORD | Dockerhub 密码 |
  | DOCKER_REPO     | Dockerhub 库名 |


<img width="1577" alt="image" src="https://user-images.githubusercontent.com/92626977/213895533-ce4bad42-a1f0-4ee4-8590-c5bbae5989c6.png">
<img width="1090" alt="image" src="https://user-images.githubusercontent.com/92626977/213895730-19a361b8-db3f-4f93-8656-325d76e5cbf9.png">
<img width="1670" alt="image" src="https://user-images.githubusercontent.com/62703343/213903422-b3183614-a36a-4b93-97f0-a381f4462b4d.png">

## 鸣谢下列作者的文章和项目:
网友 @meihao202 提供参与的资料

## 免责声明:
* 本程序仅供学习了解, 非盈利目的，请于下载后 24 小时内删除, 不得用作任何商业用途, 文字、数据及图片均有所属版权, 如转载须注明来源。
* 使用本程序必循遵守部署免责声明。使用本程序必循遵守部署服务器所在地、所在国家和用户所在国家的法律法规, 程序作者不对使用者任何不当行为负责。