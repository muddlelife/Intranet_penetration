# 内网渗透(windows常用命令)

## 基础信息收集

旨在了解当前服务器的计算机基本信息，为后续判断服务器角色，网络环境等做准备

```powershell
systeminfo  # 详细信息
net start  # 启动服务
tasklist  # 进程列表
schtasks  # 计划任务
netstat -ano  # 查看端口
whoami  # 我是谁
net user  # 查看当前系统的所有用户
net user <用户名> <用户密码> /add  # 创建用户
net localgroup administrators <用户名> /add  # 将用户加入administrators 用户组
net user <用户名>$ <用户密码> /add  # 创建隐藏用户，然后在执行net user <用户名>$ 发现用户的确存在
# 远程连接
# 首先查看远程连接的端口，执行
tasklist /svc  # 寻找TermService,得知PID
# 然后执行
netstat -ano # 寻找PID的端口，然后连接
```

旨在了解当前服务器的网络接口信息，为判断当前角色，功能，网络架构做准备

## 域信息收集

```powershell
ipconfig /all  # 判断存在域-dns
net view /domain  # 判断存在域
net time /domain  # 判断主域
netstat -ano  # 当前网络端口开放
nslookup  # 域名 追踪来源地址
net time  # 查询当前主机时间，会显示主机名
net time /domain  # 查询当前域时间，会显示域名
```

## 用户信息收集操作演示

旨在了解当前计算机或域环境下的用户及用户组信息，便于后续利用凭据进行测试

```txt
系统默认常见用户身份：
Domain Admins: 域管理员（默认对域控制器有完全控制权）
Domain Computers: 域内机器
Domain Controllers： 域控制器
Domain Guest： 域访客，权限低
Domain Users： 域用户
Enterprise Admins： 企业系统管理员用户（默认对域控制器有完全控制权）
相关用户收集操作命令：
whoami /all  用户权限
net config workstation  登录信息
net user  本地用户
net localgroup  本地用户组
net user /domain  获取域用户信息
net group /domain  获取域用户组信息
wmic useraccount get /all  涉及域用户详细信息
net group "Domain Admins" /domain  查询域管理员账户
net group "Enterprise Admins" /domain  查询管理员用户组
net group "Domain Controllers" /domain  查询域控制器
```
