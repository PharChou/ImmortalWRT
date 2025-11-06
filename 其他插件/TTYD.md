# 安装TTYD
```
opkg update
opkg install ttyd
opkg install luci-app-ttyd
```
# 设置免登录自动进入TTYD
在 OpenWrt 中安装 ttyd 后，如果你希望打开网页终端（例如 http://192.168.1.1:7681）时免输入账号密码直接登录为 root 用户，可以通过以下方式实现：
## **安全警告**
此操作会使任何访问你路由器 TTYD 地址的人 
**无需密码即获得 root 权限**
**请仅在完全受信任的本地网络中使用**
## 编辑 ttyd 的启动配置文件
```
vi /etc/config/ttyd
```
## 修改或添加以下配置项**
```
config ttyd
        option interface '@lan'
        option command '/bin/login -f root'
        option debug '7'
```
- option command '/bin/login -f root' 表示直接以 root 用户免密登录
- option interface '@lan' 表示只监听内网 LAN 接口（默认如此，增强安全）
- 也可以在配置中修改命令选项为/bin/login -f root即可
## 重启 ttyd 服务**
```
/etc/init.d/ttyd restart
```
