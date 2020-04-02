## Linux安装方法(eg Debian,Ubuntu)
### 编译
  如果需要biliip解析功能，请使用以下命令编译:

        apt-get update; apt-get install -y automake libncurses5-dev libncursesw5-dev
        ./bootstrap.sh
        ./configure --without-gtk --disable-ipv6 --with-biliip
        make -j8
        make install

  如果需要ipip.net解析功能，请使用以下命令编译:

        apt-get update; apt-get install -y automake libncurses5-dev libncursesw5-dev libjson-c-dev
        ./bootstrap.sh
        ./configure --without-gtk --disable-ipv6 --with-ipdotnet
        make -j8
        make install

### 下载IP库  
  下载以下地址中的数据文件放置至
        
        /usr/local/opt/mtr/biliip.dat
        http://wsdownload.hdslb.net/BiliIP.dat.gz

        /usr/local/opt/mtr/ipdotnet.ipdb
    
  运行时使用以下两种方式：
  
        MTR_OPTIONS="-R" mtr
        mtr -R

## MAC 安装示例
 * 原生 mtr 添加了 位置显示 和 DNS反向解析。
### 编译环境准备

>    ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"

    brew install automake
    brew install wget
    brew install gtk+
    brew install json-c
    ln -s /usr/local/Cellar/json-c/0.13.1/include/json-c/ /usr/local/Cellar/json-c/0.13.1/include/json-c/json

### 下载源码

    git clone https://github.com/Bilibili/mtr

### 编译安装 (biliIP 版本)

    cd mtr
    ./bootstrap.sh 
    ./configure --without-gtk --disable-ipv6 --with-biliip 
    make -j8
    sudo bash -c 'cp mtr /usr/local/bin && mkdir /opt/mtr && chmod +s /usr/local/bin/mtr && mkdir -p /usr/local/opt/mtr && wget http://wsdownload.hdslb.net/BiliIP.dat.gz -O - | gzip -dc > /usr/local/opt/mtrBiliIP.dat'

### 编译安装 (ipip.net 版本)

    cd mtr
    ./bootstrap.sh 
    ./configure --without-gtk --disable-ipv6 --with-ipdotnet 
    make -j8
    sudo bash -c 'cp mtr /usr/local/bin && mkdir /opt/mtr && chmod +s /usr/local/bin/mtr && mkdir -p /usr/local/opt/mtr 

    自行下载ipip.net数据库井放置于/usr/local/opt/mtr/ipdotnet.ipdb

### Show一把
#### 原生

    sudo mtr www.bilibili.com

#### 扩展

    sudo mtr -R www.bilibili.com

#### 感谢

    IP库国家/城市数据来源：http://www.ipip.net/ 免费版
    IP库ISP来源：QQWry / 新浪公开IP查询库

#### 截图

![MAC运行截图](http://ww1.sinaimg.cn/large/64bb76b9gw1ev01oyul45j20pd0b441o.jpg)