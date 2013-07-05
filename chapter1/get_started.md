
#cubieboard 基础指南

**作者: fy**

本教程适用于a10，板子上的系统是默认的linux即linaro，环境是windows xp 32bit，书写于2013.7.4

**面向对linux有一定基础的用户。**  

个人使用编辑器为vi，若不熟悉请自行在输入命令时将vi替换为nano。

主要讲解cb开发板的配置，同时部分涉及刷机等内容。


## 进入 Shell 界面  

---

### 1. 接入TTL线  

        此时不必加电开机。先将TTL线插到板子上，对应关系如下：

        Cable             Pin on Cubieboard  
        PIN1(红色)            TX  
        PIN2(绿色)            RX  
        GROUND (黑色)         GND  
  
        注意：千万别顺手把红线接到VCC上面！  

        下载并安装 PL-2303 驱动。  
        将TTL线另一端插入USB口。弹出检测到新硬件并自动识别。

### 2. 从终端接收开发板数据

        下载并安装 XShell 或 Putty 等支持连接终端的软件。  
        新建连接，调整协议为SERIAL(串口)，并设置PORT(连接对象)为非COM1的那个口。调整至能成功建立连接。  
        加电并启动开发板，终端窗口得到大量输出，最终获得一个能够输入的Shell。



## 基础配置

---

### 1. 用户  
        #首先确保自己是root帐户或，若不是，通过这个命令切过去。  
>        sudo -i

        #配置用户：
>        useradd fy
>        passwd fy

        #创建用户目录并改变所有权：
>        cd /home
>        mkdir fy

>        chgrp fy fy
>        chown fy fy

        #加入sudo组：
>        usermod -a -G sudo fy

        #配置默认终端
>        vi /etc/passwd
        将 fy:x:1001:1002::/home/fy:/bin/sh 末尾修改为 /bin/bash

### 2. 网络  

        插网线。  

        迅速连入网络：
>        vi /etc/network/interfaces  

        加入一行：
>        nameserver 8.8.8.8  

        保存，重启网络服务：
>        /etc/init.d/network restart

        固定IP的个人配置：
>><pre>
auto eth0
iface eth0 inet static
    address 192.168.1.7
    gateway 192.168.1.1
    netmask 255.255.255.0
auto lo
iface lo inet loopback
</pre>

### 3.  SSH配置及其他软件的安装
        开始时候可能会无法进行软件安装。df -h 看一下磁盘占用率可以得知磁盘已满。  
        你可能很快就会发现空间总数加起来达不到标称的4GB，这是因为有一部分nand没有被划入分区。  
        这一点比较好解决。首先通过  
>        fdisk
        和df命令看一下当前的分区，确定根分区。一般来说，根分区是 /dev/nandc  
        那么可以直接执行：  
>        resize2fs /dev/nandc

        如果正确就会看到可用空间顺利扩大，那么现在可以进行接下来的操作了。

        #首先更新源  
>        apt-get update  
>        apt-get install openssh-server  

        #此时如无意外，用ifconfig看一下开发板IP，你已经可以通过 xshell 或 putty 等软件连接开发板了。
        #如果ssh在安装完成后没有正确工作，重启一下ssh服务即可。
>        #/etc/init.d/ssh restart  

        #连上SSH以后，TTL线可以收起来。

        #个人向的软件安装列表，看看就好  
>        apt-get install vim
>        #apt-get install python
>        apt-get install python-tornado 
>        apt-get install sqlite3 
>        apt-get install ack-grep
>        

### 4. 中文配置  

        默认情况下，在vim中输入中文会变成乱码，这可以通过本地化配置来解决。

        对于第一个文件的文件名，我记不太清了。但可以确定在debian下应修改 /etc/locale.gen 。请诸位核实一下然后向我反馈。

>        vi /var/lib/locales/supported.d/local

>><pre>
en_US.UTF-8 UTF-8
zh_CN.UTF-8 UTF-8
zh_CN.GBK GBK
zh_CN GB2312
</pre>

        重新配置locale  
>        locale-gen  

        完成后继续编辑下一个文件：  
>        vi /etc/default/locale
>><pre>
LANG="zh_CN.UTF-8
LANGUAGE="zh_CN:zh"
LC_NUMERIC="zh_CN.UTF-8"
LC_TIME="zh_CN.UTF-8"
LC_MONETARY="zh_CN.UTF-8"
LC_PAPER="zh_CN.UTF-8"
LC_NAME="zh_CN.UTF-8"
LC_ADDRESS="zh_CN.UTF-8"
LC_TELEPHONE="zh_CN.UTF-8"
LC_MEASUREMENT="zh_CN.UTF-8"
LC_IDENTIFICATION="zh_CN.UTF-8"
</pre>

### 5. 时区  

        我们是东八区(UTC+8)。更换设置文件后进行时间同步。

>        cp /usr/share/zoneinfo/Asia/ShangHai /etc/localtime 

>        #cp /usr/share/zoneinfo/Asia/Shanhai /etc/localtime  #debian下是这样的

>        ntpdate cn.pool.ntp.org 

### 6. sudo 问题

        在使用 sudo 的时候可能会总是遇到这样一行提示：  
>        sudo:unable to resolve host cubieboard

        解决方法：
>><pre>
vi /etc/hosts
127.0.0.1 localhost cubieboard
</pre>

        cubieboard 是主机名(hostname)


## 扩展内容

---

### 1. 远程桌面 - xrdp  
        请注意，从现在开始我要胡扯了。xrdp的资料凭着记忆给出，不保证其准确性。  
        如经测试，请立即向我反馈结果。
  
        xrdp的配置较为简单。不过个人认为效果不是很好。卡顿之类比较明显，还有色彩缺失的问题。

>        apt-get install xrdp

        开始->运行，输入mstsc，回车。  
        这时应该能够连接上开发板并可以输入账号密码。  
        但在连接时会遇到：error - problem connecting.  

>        vi /etc/xrdp/startwm.sh  

        将最后一句：
>        . /etc/X11/Xsession

        修改为：
>        startlubuntu &

        重新使用 mstsc 进行连接，成功进入桌面。


### 2. 如何刷机(Nand)  

        准备工作：microUSB数据线一根、TTL线(非必要)、系统镜像  

        刷机需要 PhoenixSuit 或者 LiveSuit 软件，这里推荐 PhoenixSuit。

        安装好刷机工具后按照下面的步骤做：

        0. 关闭开发板，拔掉电源线。  

        1. 打开刷机工具，预先选好镜像文件。  

        2. 将开发板从外壳中取出（不这样做数据线插不牢）。  

        3. 将数据线一端插入开发板，用手按着板子上的 FEL 按钮，保持这个状态不要放手，将另一端插入电脑上的USB口。  

        4. 在这个过程中，开发板将会被点亮，同时电脑上会弹出找到新硬件向导。按住FEL键不要放手直到驱动安装完成，刷机软件会提示你可以刷机。

        5. 这时候可以松手了，等到写入完成后重启开发板即可。操作系统已经被刷入。  

>**在驱动安装完成前千万不要松手。如果驱动安装失败，那么在设备管理器里找USB，删掉刚才装的带问号的驱动重新来过。**  
>**如果你的操作系统是linux，英文官网上点Doc，有一个五分钟刷机的文档。**

### 3. 把系统刷进microSD(TF)卡

        你需要两样东西：win32diskimager 和 系统镜像

        插卡后启动 win32diskimager，选了镜像直接点 Write 即可。 


  

## 推荐系统及其配置 - Cubian

---

### 0. 何为 Cubian，又为何推荐

        [关于 Cubian](https://github.com/cubieplayer/Cubian)

        这个系统吸引我之处在于其干净整洁，对我来说我可以随便折腾，把它弄成我想要弄成的样子，这非常好。  

        不像是 ubuntu server 之流，默认就带个apache2带个mysql什么的，对于小板子来说太重了。  

        尽管从默认集成了perl(似乎如此)而没有python这一点看来，作者估计py教徒的我不是一个路数。  

        但是除了这个之外，就只有刚启动时候那个猴子LOGO不甚给力了。  


### 1. 如何安装

        首先下载镜像，截止我写文章有三个版本：r1 r2 r3，直取r3即可。  

        [下载地址](http://cubieplayer.github.io/Cubian/dist/)  

        然后安装 win32diskimager 按上面教的步骤把系统刷进sd卡。  

        插卡启动开发板，这就进入了Cubian系统。  

        ls一下 你可以看到有个nandinstall目录。  

        执行里头的 install.sh 就可以直接将其刷入nand了。  

### 2. 重新分区

        但是不要急着做这件事情，我们可以通过编辑这个文件来修改一下配置。  

        cubian默认分了三个区：nanda nandb nandc  

        其中nanda是引导分区，占空间很小。b和c则各占2G空间，nandb是根分区，nandc则挂在/mnt/nandc打酱油。  

        那么我打算去掉nandc 让根分区大一点，按如下流程来做：  

        1. 搜索NANDC和nandc，删除 mkfs 处有关的一行和fstab处有关的两行。

        2. 搜索NANDPART，找到这句话：

>        $NANDPART $NAND 16 "boot 2048" "linux 4000000" "data 0"

        修改为：  

>        $NANDPART $NAND 16 "boot 2048" "linux 0"  

        0代表余下全部。这里的单位1是512byte，所以可知boot分区在分区表中的大小是1MB。

        此外，cubian r3默认会将nand格式化为ext4，但是ext4文件系统的日志会造成频繁存取从而损害nand寿命。我们可以将其关闭：  

        1. 搜索 mkfs.ext4 找到：

>        mkfs.ext4 $NANDB  

        修改为：  

>        mkfs.ext4 -O ^has_journal $NANDB  

        2. 保存并执行。等待安装完成。

### 3. 其他  

        cubian 需要注意一点，就是非root帐户看不到需要root权限执行的大多数命令，例如halt或reboot。  

        这些命令并不是不存在了。这点需要惯用其他发行版的用户特别注意。

        可以用 export PATH=/sbin:/usr/sbin:$PATH 来获得临时解决。  

        配置流程与上头基本相同。

