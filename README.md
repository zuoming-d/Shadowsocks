# 使用KiwiVM面板搭建Shadowsocks

### 前期准备

* 获得一个境外服务器，如搬瓦工 <http://bandwagonhost.com>
* 安装操作系统 CentOS 6

### 如何搭建

#### 1. 安装EPEL源
```
wget http://download.fedoraproject.org/pub/epel/6/x86_64/epel-release-6-8.noarch.rpm
rpm -ivh epel-release-6-8.noarch.rpm
```

#### 2. 安装pip
```
yum install python-pip -y
```

#### 3. 安装Shadowsocks
```
pip install shadowsocks
```

#### 4. 创建配置文件
```
mkdir /etc/shadowsocks/
vi /etc/shadowsocks/config.json
```
把config.json改成如下形式:

```
{
   "server":"0.0.0.0",
    "server_port":443,
    "password":"yourpassword",
    "timeout":600,
    "method":"aes-256-cfb",
    "workers":5
}
```
编辑完成后键入 `:wq` 保存并退出

#### 5. 运行Shadowsocks

来到`config.json`所在文件夹

```
cd /etc/shadowsocks
ssserver
```
为了每次开机自动启动Shadowsocks，我们更改开机脚本`/etc/rc.local`。在结尾加上：

```
nohup ssserver -c /etc/shadowsocks/config.json &
```
Reboot后就可以使用Shadowsocks了

查看状态：

```
netstat -anp
```