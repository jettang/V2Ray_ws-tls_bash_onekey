# V2Ray 基于 Nginx 的 vmess+ws+tls 一键安装脚本

* V2Ray是一个优秀的开源网络代理工具，可以帮助你畅爽体验互联网，目前已经全平台支持Windows、Mac、Android、IOS、Linux等操作系统的使用。

## 本脚本目前支持 Centos7 + / Debian 8+ / Ubuntu 16.04+ 
## 请用户根据该文档及时更新 V2ray core，否则有可能会出现 客户端无法连接到服务端 的情况
* 本脚本默认安装最新版本的V2ray core
* 本脚本的第一批用户安装的内核为 V2ray core 3.6 版本，请该内核版本的用户，根据下文及时更新内核版本。
* V2ray core 3.8 修复了一个导致 mKCP 初始速度慢的问题。
* V2ray core 目前最新版本为 3.10

## V2ray core 更新方式
执行：
`bash <(curl -L -s https://install.direct/go.sh)`

（ 来源参考 ：[V2ray官方说明](https://www.v2ray.com/chapter_00/install.html)）
* 如果为最新版本，会输出提示并停止安装。否则会自动更新
* 未来会将相关内容集成到本脚本中并进行交互式操作更新

## 注意事项
* 推荐在纯净环境下使用本脚本，如果你是新手，请不要使用Centos系统。
* 在尝试本脚本确实可用之前，请不要将本程序应用于生产环境中。
* 该程序依赖 Nginx 实现相关功能，请使用 [LNMP](https://lnmp.org) 或其他类似携带 Nginx 脚本安装过 Nginx 的用户特别留意，使用本脚本可能会导致无法预知的错误（未测试，若存在，后续版本可能会处理本问题）。
* V2Ray 的部分功能依赖于系统时间，请确保您使用V2RAY程序的系统 UTC 时间误差在三分钟之内，时区无关。
* 本 bash 依赖于 [V2ray 官方安装脚本](https://install.direct/go.sh) 及 [acme.sh](https://github.com/Neilpang/acme.sh) 工作。
* Centos 系统用户请预先在防火墙中放行程序相关端口（默认：80，443）
## 准备工作
* 准备一个域名，并将A记录添加好。
* [V2ray官方说明](https://www.v2ray.com/)，了解 TLS WebSocket 及 V2ray 相关信息
* 安装好 git
## 安装方式
```
git clone https://github.com/wulabing/V2Ray_ws-tls_bash_onekey.git temp && cd temp && bash install.sh | tee v2log.txt
```
## 启动方式

启动 V2ray：`systemctl start v2ray`

启动 Nginx：`systemctl start nginx`

（其他的应该不用我多说了吧 嘿嘿嘿）


### 测试说明
* 该测试为 V2.0 版本在 Vultr 测试机使用官方模板进行的测试
* 理论上支持所有具备 Systemd 特性的开发版系统

| NO | Status| Platform|
|----|-------|---------|
|1|PASS|Centos 7|
|2|PASS|Debian 8|
|3|PASS|Debian 9|
|4|PASS|Ubuntu 16.04|
|5|PASS|Ubuntu 17.04|
### 问题反馈
* 请携带 v2log.txt 文件内容进行反馈
### 更新说明
## 2018-02-04
V2.1.1(stable)
* 1.变更 local_ip 判断方式，从 本地网卡获取 变更至 命令获取 公网IP。
* 1.修复 域名dns解析IP 与 本机IP 不匹配 误报问题
## 2018-01-28
v2.1.1(stable)
* 1.修复 缺乏 lsof 依赖导致的端口占用判断异常问题
## 2018-01-27
v2.1.1(stable）
* 1.修复 部分机型因缺乏 crontab （计划任务）依赖导致的安装失败问题
* 2.完善 端口占用 判断
## 2017-12-06
V2.1（stable）
* 1.修复 Centos7 找不到 Nginx 安装包的问题
* 2.完善 SElinux 配置过程提醒标识

V2.0（stable）
* 1.增加 Centos7 系统支持
* 2.增加 自定义端口 和 自定义alterID
* 3.完善 安装所需依赖
* 4.修复 Ubuntu 系列系统版本判断异常导致的安装中断问题
* 5.修复 bug

V1.02（beta）
* 1.增加 系统判定，目前打算仅支持带systemd的较新主流开发版系统
* 2.本机 IP 获取方式重构

## 2017-12-05

V1.01（beta）
* 1.完善 支持 Debian9
* 2.修复 由于 Debian9 默认未安装 net-tools 导致的本机ip判定错误
* 3.修复 bc 安装问题
* 4.增加 ip 判定不一致时继续安装的选项（由于某些vps情况比较特殊，判定到内网IP或本身网卡信息，或公网ip与服务期内信息不一致等情况）

V1.0（beta）
* 1.目前仅支持 Debian 8+ / Ubuntu 16.04+ 
* 2.逐渐完善中
