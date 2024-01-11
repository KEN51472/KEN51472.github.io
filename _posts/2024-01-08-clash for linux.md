---
layout: detail
type : 5
keyword : clash
title: clash for linux
description: 
---

## clash 安装

安装 

`git clone https://github.com/wanhebin/clash-for-linux.git`

## clash 使用

修改clash_url   
`vim .env`

运行脚本文件   
`sudo bash start.sh`

脚本运行结果如下   
```
CPU architecture: amd64

正在检测订阅地址...
Clash订阅地址可访问！                                      [  OK  ]

正在下载Clash配置文件...
配置文件config.yaml下载成功！                              [  OK  ]

判断订阅内容是否符合clash配置文件标准:
订阅内容符合clash标准

正在启动Clash服务...
服务启动成功！                                             [  OK  ]

Clash Dashboard 访问地址: http://<ip>:9090/ui
Secret: xxxx

请执行以下命令加载环境变量: source /etc/profile.d/clash.sh

请执行以下命令开启系统代理: proxy_on

若要临时关闭系统代理，请执行: proxy_off

```
检查服务端口   
`netstat -tln | grep -E '9090|789.'`

检查环境变量   
`env | grep -E 'http_proxy|https_proxy'`

网络代理设置   
<img src="/pics/24_01_08_1.png" alt="Description of the image" style="max-width:100%">

## Clash Dashboard

打开 http://localhost:9090/ui/   

<img src="/pics/24_01_08_2.png" alt="Description of the image" style="max-width:80%">
                                             
secret处输入脚本运行时输出的secret码

成功后页面   
<img src="/pics/24_01_08_3.png" alt="Description of the image" style="max-width:70%">


## 相关链接

[配置教程](https://www.chenhaifei.com/?p=2005)  