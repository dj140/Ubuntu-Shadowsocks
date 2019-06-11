# Ubuntu-Shadowsocks

# ubuntu（客户端）配置shadowsocks
# 安装ss

    sudo apt-get update
    sudo apt-get install Python-gevent python-pip
    pip install shadowsocks
# 配置ss
    vim /etc/ss.json
    以下内容为配置文件demo

    {
      "server":"服务器ip",
      "server_port":服务器端口,
      "local_port":1080,
      "password":"密码",
      "timeout":600,
      "method":"aes-256-cfb"
    }
# 启动ss

    sslocal -c /etc/ss.json 

# 设置开机启动

    gnome-session-properties
    
在弹出的窗口里填写

添加(Add) -> 名称(name)和描述(comment)随便填

命令(Command)填写如下：

    nohup sslocal -c /etc/ss.json &
---------------------------------------------------------------------------------------------------------

# 配置polipo

# 安装polipo

    sudo apt-get install polipo
    
# 配置polipo

    sudo vim /etc/polipo/config
    配置文件如下

    # Uncomment this if you want to use a parent SOCKS proxy:

    socksParentProxy = "localhost:1080"

    socksProxyType = socks5

# 重启polipo服务

    sudo service polipo stop
    sudo service polipo start
---------------------------------------------------------------------------------------------------------

# 配置终端

    vim ~/.bashrc
    
    增加如下配置

    alias gfw="http_proxy=http://localhost:8123"
    
    source ~/.bashrc
    
# 测试一下
    
    sudo apt-get install curl
    curl ip.gs
    当前 IP：xxx.xxx.xxx.xxx 来自：中国安徽马鞍山 电信
    gfw curl ip.gs
    当前 IP：xxx.xxx.xxx.xxx 来自：日本东京
--------------------------------------------------------------------------------------------------------------

# git配置代理

    vim ~/.bashrc
    
    增加如下配置
    fk=" --config http.proxy=localhost:8123"
    
    source ~/.bashrc

# 测试一下

    git clone  https://android.googlesource.com/tools/repo $sw

    export http_proxy=http://127.0.0.1:8123
    export https_proxy=http://127.0.0.1:8123
    export ftp_proxy=http://127.0.0.1:8123
