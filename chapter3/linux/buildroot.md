<CENTER> 用buildroot构建embedded linux系统 </CENTER>
=============================================

# 简单说明:

1. 所有操作基于ubuntu 12.04(x86_64)
2. 采用linux-sunxi最新的linux-3.4内核
3. buildroot版本号选取目前最新发布的buildroot 2013-02
4. 最终固件包采用livesuit烧录到cb的nand存储介质中

# 获取源代码

##创建工作目录

<pre>    $mkdir ~/mylinux
    $cd ~/mylinux </pre>

##采用git下载最新代码

<pre>    $git clone git://github.com/cubieboard/sunxi-tools.git tools
    $git clone git://github.com/cubieboard/u-boot-sunxi.git u-boot
    $git clone git://github.com/cubieboard/buildroot-sunxi.git buildroot
    $git clone git://github.com/cubieboard/linux-sunxi.git linux-3.4 </pre>

##切换到sunxi-3.4-cb分支

<pre>    $(cd tools; git checkout -b sunxi-3.4-cb origin/sunxi-3.4-cb)
    $(cd u-boot; git checkout -b sunxi-3.4-cb origin/sunxi-3.4-cb)
    $(cd buildroot; git checkout -b sunxi-3.4-cb origin/sunxi-3.4-cb)
    $(cd linux-3.4; git checkout -b sunxi-3.4-cb origin/sunxi-3.4-cb) </pre>

# 编译并生成固件

<pre>   $cd ~/mylinux
   $tools/build.sh (注意：不要进到tools目录下执行build.sh) </pre>

# 把固件烧写进cubieboard

1. 启动livesuit程序，选中在tools/pack下面生成的固件
2. 按住靠近以太网侧的按键，并保持住
3. 插入macro USB线，等livesuit有响应后松开按键
4. 进入烧写模式，烧写完就可以启动到自己定制的linux系统了

# 定制方法说明

## 裁剪buildroot

我们知道，buildroot包含了大量的软件包，我们仅需要把我们关心的软件包选住， buildroot将自动帮你把软件加入到你的linux系统中，下面的简单的步骤

<pre>    $cd ~/mylinux/buildroot
    $make cubieboard_defconfig
    $make menuconfig
    $这里出现经典的ncurse界面，使用上下左右+空格等选择软件包，退出并保存
    $cp .config configs/cubieboard_defconfig  (自动化编译脚本将从configs中复制cubieboard_defconfig文件) </pre>


## 定制nand分区大小

我们知道, cubieboard上的nandflash的容量是4GB。当前nand的分区情况可以看～/mylinux/tools/pack/chips/sun4i/configs/linux/default/下面的sys_config.fex文件，如下面所示

<pre>    [part_num]
    num     = 4
    [partition0]
        class_name  = DISK
        name        = bootloader
        size_hi     = 0
        size_lo     = 32768
        user_type   = 0
        ro          = 0
    [partition1]
        class_name  = DISK
        name        = env
        size_hi     = 0
        size_lo     = 16384
        user_type   = 0
        ro          = 0
    [partition2]
        class_name  = DISK
        name        = boot
        size_hi     = 0
        size_lo     = 16384
        user_type   = 0
        ro          = 0
    [partition3]
        class_name  = DISK
        name        = rootfs
        size_hi     = 0
        size_lo     = 524288
        user_type   = 0
        ro          = 0 </pre>
    
num= 4表示分为4个分区，每个分区的容量由size_lo指定，以1KB为单位。需要注意的是，如果4个分区的容量没有用完4GB（我们的nandflash是4GB），则烧写的时候会自动添加一个分区，用完所有的nand容量。我们进入linux系统，看一下系统中的分区，如下：

<pre>    [root@linux ~]# ls -l /dev/nand*
    brw-------    1 root     root       93,   0 Jan  1  1970 /dev/nand
    brw-------    1 root     root       93,   1 Jan  1  1970 /dev/nanda
    brw-------    1 root     root       93,   2 Jan  1  1970 /dev/nandb
    brw-------    1 root     root       93,   3 Jan  1  1970 /dev/nandc
    brw-------    1 root     root       93,   4 Jan  1  1970 /dev/nandd
    brw-------    1 root     root       93,   5 Jan  1  1970 /dev/nande </pre>
    
其中/dev/nand表示的是整个nand设备，容量是4GB，nanda,nandb,nandc,nandd是sys_config.fex中配置的分区，nande是系统计算剩余容量自动创建的。在使用livesuit烧写的时候，每个用户分区要烧写的镜像也是在sys_config.fex中指定的，如下
    
<pre>    [down_num]
    down_num    = 4
    
    [download0]
    part_name   = bootloader
    pkt_name    = BOOTLOADER_00000
    encrypt     = 0
    
    [download1]
    part_name   = env
    pkt_name    = ENVIROMENT_00000
    encrypt     = 0
    
    [download2]
    part_name   = boot
    pkt_name    = KERNEL_000000000
    encrypt     = 0
    
    [download3]
    part_name   = rootfs
    pkt_name    = ROOTFS_000000000
    encrypt     = 0 </pre>

比如前面的bootloader分区，它的索引名是BOOTLOADER_00000，在相同目录下的image.cfg中找到下面一行

<pre>    {filename = "bootloader.fex",   maintype = ITEM_ROOTFSFAT16,  subtype = "BOOTLOADER_00000",}, </pre>

从上面我们可以发现，bootloader区下载的是bootloader.fex文件，我们可以仔细研究tools/pack/pack脚本，发现bootloader.fex是fsbuild命令工具创建的一个fat16的文件镜像，它们内容来源于~/mylinux/tools/pack/chips/sun4i/wboot/bootfs。同理，其他的分区文件也可以这样分析。这里举个简单的例子，把nandd(也就是我们linux的根分区）容量从原来的512MB调整到2GB
，只需要在sys_config.fex的

<pre>    [partition3]
    class_name  = DISK
    name        = rootfs
    size_hi     = 0
    size_lo     = 524288
    user_type   = 0
    ro          = 0
    改为
    [partition3]
    class_name  = DISK
    name        = rootfs
    size_hi     = 0
    size_lo = 2057152
    user_type   = 0
    ro          = 0 </pre>

然后重修执行tools/build.sh,烧写完进入系统，nandd的容量就变成2GB了。

## 裁剪linux内核

如果自己添加了内核模块或者想要加入其他现成的内核模块可以参考下面的做法

<pre>    $cd ~/mylinux/linux-3.4
    $cp arch/arm/configs/cubieboard_defconfig .config
    $make ARCH=arm menuconfig (注意：不要漏了ARCH=arm)
    执行完上面的命令后，则进入经典的NCURSE界面，选上自己喜欢的驱动后，退出，再把新的配置文件保存
    $cp .config arch/arm/configs/cubieboard_defconfig </pre>


# 贡献您的开发

欢迎任何人参与开发，如果有什么疑问，可以发邮件到matson@cubietech.com
