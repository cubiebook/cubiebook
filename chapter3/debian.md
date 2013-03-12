<h2 align="CENTER"   style="page-break-before: auto; page-break-after: auto;"   >&nbsp;一步步安装<font face="Arial, Liberation Sans, sans-serif"   ><span lang="en-US"   >CubieBoard</span></font>最小系统<font face="Arial, Liberation Sans, sans-serif"   >
</font><font face="Arial, Liberation Sans, sans-serif"   ><span lang="en-US"   >v1.1</span></font></h2>
<p align="RIGHT"   style="margin-bottom: 0cm;"   ><font size="1"   style="font-size: 8pt;"   ><span lang="en-US"   ><font color="#0000ff"   ><a href="http://onefishum.blog.163.com/blog/static/5184730520131151385937/"   >http://onefishum.blog.163.com/blog/static/5184730520131151385937/</a></font></span></font></p>
<p style="margin-bottom: 0cm;"   ><br>
</p>
<p style="margin-bottom: 0cm;"   ><font color="#ff0000"   >定义及标准：</font></p>
<ol>
	<li><p style="margin-bottom: 0cm;"   ><font color="#ff0000"   >所有操作基于<span lang="en-US"   >ubuntu
	12.10 root</span>用户。</font></p>
	</li><li><p style="margin-bottom: 0cm;"   ><font color="#ff0000"   >所有备注用红色字体。</font></p>
	</li><li><p style="margin-bottom: 0cm;"   ><font color="#ff0000"   >用户输入使用蓝色字体。</font></p>
	</li><li><p style="margin-bottom: 0cm;"   ><font color="#ff0000"   >硬盘至少<span lang="en-US"   >4G</span>以上的剩余空间。</font></p>
	</li><li><p style="margin-bottom: 0cm;"   ><font color="#ff0000"   ><span lang="en-US"   >TF</span>卡<span lang="en-US"   >512M</span>以上</font></p>
	</li><li><p style="margin-bottom: 0cm;"   ><font color="#ff0000"   >教程制做内核版本为<span lang="en-US"   >Linux-3.0.62+</span></font></p>
	</li><li><p style="margin-bottom: 0cm;"   ><font color="#ff0000"   >默认路径为<span lang="en-US"   >/root</span>目录。</font></p>
</li></ol>
<p style="margin-bottom: 0cm;"   ><br>
</p>
<p style="margin-bottom: 0cm;"   ><font color="#ff0000"   >更新：</font></p>
<p style="text-indent: 0.71cm; margin-bottom: 0cm;"   ><font color="#ff0000"   ><span lang="en-US"   >1.1</span>版本</font></p>
<p style="text-indent: 0.71cm; margin-bottom: 0cm;"   ><font color="#ff0000"   >发现<span lang="en-US"   >linux</span>分区兼容性。一些杂牌卡，可能分区会有问题，尽量用品牌。此问题为<span lang="en-US"   >linux</span>下分区软件的问题。本文使用为<span lang="en-US"   >sandisk</span>的卡。</font></p>
<p style="margin-bottom: 0cm;"   ><br>
</p>
<p style="margin-bottom: 0cm;"   ><br>
</p>
<ol>
	<li><p style="margin-bottom: 0cm;"   ><b>在</b><span lang="en-US"   ><b>ubuntu
	</b></span><b>下安装如下软件，主要用于编译源码及基础系统安装</b></p>
</li></ol>
<p align="JUSTIFY"   style="text-indent: 0.74cm; margin-bottom: 0cm; line-height: 100%; page-break-inside: auto; widows: 0; orphans: 0; page-break-before: auto; page-break-after: auto;"   >
<span lang="en-US"   ># <font color="#000080"   >apt-get install
build-essential u-boot-tools qemu-user-static debootstrap
emdebian-archive-keyring git libusb-1.0-0-dev pkg-config</font></span></p>
<p align="JUSTIFY"   style="text-indent: 0.74cm; margin-bottom: 0cm; line-height: 100%; page-break-inside: auto; widows: 0; orphans: 0; page-break-before: auto; page-break-after: auto;"   >
<span lang="en-US"   ># <font color="#000080"   >apt-get install
gcc-arm-linux-gnueabihf</font>  ; pc </span>交差编译<font face="Times New Roman, Liberation Serif"   >
</font><span lang="en-US"   >arm </span>系统。</p>
<p align="JUSTIFY"   style="text-indent: 0.74cm; margin-bottom: 0cm; line-height: 100%; page-break-inside: auto; widows: 0; orphans: 0; page-break-before: auto; page-break-after: auto;"   >
<br>
</p>
<ol start="2"   >
	<li><p style="margin-bottom: 0cm;"   ><b>制做</b><span lang="en-US"   ><b>TF</b></span><b>卡</b></p>
</li></ol>
<ol>
	<li><p style="margin-bottom: 0cm;"   >插上<span lang="en-US"   >TF</span>卡后</p>
</li></ol>
<p style="text-indent: 0.74cm; margin-bottom: 0cm;"   >查看<span lang="en-US"   >TF</span>信息</p>
<p style="text-indent: 0.74cm; margin-bottom: 0cm;"   ><span lang="en-US"   >#
<font color="#000080"   >ls /dev/mmcblk0*</font></span></p>
<p style="text-indent: 0.74cm; margin-bottom: 0cm;"   ><span lang="en-US"   >/dev/mmcblk0
 /dev/mmcblk0p1</span></p>
<p style="text-indent: 0.74cm; margin-bottom: 0cm;"   ><font color="#ff0000"   >注：可能你的显示不是以下信息。但至少有<span lang="en-US"   >/dev/mmcblk0</span>，说明你的<span lang="en-US"   >tf</span>已经被系统实别。注意，<span lang="en-US"   >ubuntu</span>系统默认有<span lang="en-US"   >TF</span>插入后会自动<span lang="en-US"   >mount</span>，请弹出不要挂载目录，以免无法进行以下操作。</font></p>
<p style="text-indent: 0.74cm; margin-bottom: 0cm;"   ><span lang="en-US"   ><font color="#000000"   >#
</font><font color="#000080"   >dd if=/dev/zero of=/dev/mmcblk0  bs=1M
count=1</font></span></p>
<p style="text-indent: 0.74cm; margin-bottom: 0cm;"   >记录了<span lang="en-US"   >1+0
</span>的读入</p>
<p style="text-indent: 0.74cm; margin-bottom: 0cm;"   >记录了<span lang="en-US"   >1+0
</span>的写出</p>
<p style="text-indent: 0.74cm; margin-bottom: 0cm;"   ><span lang="en-US"   >1048576</span>字节<span lang="en-US"   >(1.0
MB)</span>已复制，<span lang="en-US"   >0.118967 </span>秒，<span lang="en-US"   >8.8
MB/</span>秒</p>
<p style="text-indent: 0.74cm; margin-bottom: 0cm;"   ><br>
</p>
<p style="text-indent: 0.74cm; margin-bottom: 0cm;"   ><span lang="en-US"   >TF</span>卡分区</p>
<p style="text-indent: 0.74cm; margin-bottom: 0cm;"   ><font color="#000080"   ><span lang="en-US"   >#
sfdisk --in-order -uM /dev/mmcblk0</span></font></p>
<p style="text-indent: 0.74cm; margin-bottom: 0cm;"   ><span lang="en-US"   >Checking
that no-one is using this disk right now ...</span></p>
<p style="text-indent: 0.74cm; margin-bottom: 0cm;"   ><span lang="en-US"   >OK</span></p>
<p style="text-indent: 0.74cm; margin-bottom: 0cm;"   ><br>
</p>
<p style="text-indent: 0.74cm; margin-bottom: 0cm;"   ><span lang="en-US"   >Disk
/dev/mmcblk0: 486192 cylinders, 4 heads, 16 sectors/track</span></p>
<p style="text-indent: 0.74cm; margin-bottom: 0cm;"   ><br>
</p>
<p style="text-indent: 0.74cm; margin-bottom: 0cm;"   ><span lang="en-US"   >sfdisk:
ERROR: sector 0 does not have an msdos signature</span></p>
<p style="text-indent: 0.74cm; margin-bottom: 0cm;"   > <span lang="en-US"   >/dev/mmcblk0:
unrecognized partition table type</span></p>
<p style="text-indent: 0.74cm; margin-bottom: 0cm;"   ><span lang="en-US"   >Old
situation:</span></p>
<p style="text-indent: 0.74cm; margin-bottom: 0cm;"   ><span lang="en-US"   >No
partitions found</span></p>
<p style="text-indent: 0.74cm; margin-bottom: 0cm;"   ><span lang="en-US"   >Input
in the following format; absent fields get a default value.</span></p>
<p style="text-indent: 0.74cm; margin-bottom: 0cm;"   ><span lang="en-US"   >&lt;start&gt;
&lt;size&gt; &lt;type [E,S,L,X,hex]&gt; &lt;bootable [-,*]&gt;
&lt;c,h,s&gt; &lt;c,h,s&gt;</span></p>
<p style="text-indent: 0.74cm; margin-bottom: 0cm;"   ><span lang="en-US"   >Usually
you only need to specify &lt;start&gt; and &lt;size&gt; (and perhaps
&lt;type&gt;).</span></p>
<p style="text-indent: 0.74cm; margin-bottom: 0cm;"   ><br>
</p>
<p style="text-indent: 0.74cm; margin-bottom: 0cm;"   ><span lang="en-US"   >/dev/mmcblk0p1
:<font color="#000080"   >1,16,c</font></span></p>
<p style="text-indent: 0.74cm; margin-bottom: 0cm;"   ><span lang="en-US"   >/dev/mmcblk0p1
        1     16     16      16384    c  W95 FAT32 (LBA)</span></p>
<p style="text-indent: 0.74cm; margin-bottom: 0cm;"   ><span lang="en-US"   >/dev/mmcblk0p2
:<font color="#000080"   >,,L</font></span></p>
<p style="text-indent: 0.74cm; margin-bottom: 0cm;"   ><span lang="en-US"   >/dev/mmcblk0p2
       17  15193- 15177-  15540736   83  Linux</span></p>
<p style="text-indent: 0.74cm; margin-bottom: 0cm;"   ><span lang="en-US"   >/dev/mmcblk0p3
:</span></p>
<p style="text-indent: 0.74cm; margin-bottom: 0cm;"   ><span lang="en-US"   >/dev/mmcblk0p3
        0      -      0          0    0  Empty</span></p>
<p style="text-indent: 0.74cm; margin-bottom: 0cm;"   ><span lang="en-US"   >/dev/mmcblk0p4
:</span></p>
<p style="text-indent: 0.74cm; margin-bottom: 0cm;"   ><span lang="en-US"   >/dev/mmcblk0p4
        0      -      0          0    0  Empty</span></p>
<p style="text-indent: 0.74cm; margin-bottom: 0cm;"   ><span lang="en-US"   >New
situation:</span></p>
<p style="text-indent: 0.74cm; margin-bottom: 0cm;"   ><span lang="en-US"   >Units
= mebibytes of 1048576 bytes, blocks of 1024 bytes, counting from 0</span></p>
<p style="text-indent: 0.74cm; margin-bottom: 0cm;"   ><br>
</p>
<p style="text-indent: 0.74cm; margin-bottom: 0cm;"   >   <span lang="en-US"   >Device
Boot Start   End    MiB    #blocks   Id  System</span></p>
<p style="text-indent: 0.74cm; margin-bottom: 0cm;"   ><span lang="en-US"   >/dev/mmcblk0p1
        1     16     16      16384    c  W95 FAT32 (LBA)</span></p>
<p style="text-indent: 0.74cm; margin-bottom: 0cm;"   ><span lang="en-US"   >/dev/mmcblk0p2
       17  15193- 15177-  15540736   83  Linux</span></p>
<p style="text-indent: 0.74cm; margin-bottom: 0cm;"   ><span lang="en-US"   >/dev/mmcblk0p3
        0      -      0          0    0  Empty</span></p>
<p style="text-indent: 0.74cm; margin-bottom: 0cm;"   ><span lang="en-US"   >/dev/mmcblk0p4
        0      -      0          0    0  Empty</span></p>
<p style="text-indent: 0.74cm; margin-bottom: 0cm;"   ><span lang="en-US"   >Warning:
no primary partition is marked bootable (active)</span></p>
<p style="text-indent: 0.74cm; margin-bottom: 0cm;"   ><span lang="en-US"   >This
does not matter for LILO, but the DOS MBR will not boot this disk.</span></p>
<p style="text-indent: 0.74cm; margin-bottom: 0cm;"   ><span lang="en-US"   >Do
you want to write this to disk? [ynq] <font color="#000080"   >y</font></span></p>
<p style="text-indent: 0.74cm; margin-bottom: 0cm;"   ><span lang="en-US"   >Successfully
wrote the new partition table</span></p>
<p style="text-indent: 0.74cm; margin-bottom: 0cm;"   ><br>
</p>
<p style="text-indent: 0.74cm; margin-bottom: 0cm;"   ><span lang="en-US"   >Re-reading
the partition table ...</span></p>
<p style="text-indent: 0.74cm; margin-bottom: 0cm;"   ><br>
</p>
<p style="text-indent: 0.74cm; margin-bottom: 0cm;"   ><span lang="en-US"   >If
you created or changed a DOS partition, /dev/foo7, say, then use
dd(1)</span></p>
<p style="text-indent: 0.74cm; margin-bottom: 0cm;"   ><span lang="en-US"   >to
zero the first 512 bytes:  dd if=/dev/zero of=/dev/foo7 bs=512
count=1</span></p>
<p style="text-indent: 0.74cm; margin-bottom: 0cm;"   ><span lang="en-US"   >(See
fdisk(8).)</span></p>
<p style="text-indent: 0.74cm; margin-bottom: 0cm;"   ><br>
</p>
<p style="text-indent: 0.74cm; margin-bottom: 0cm;"   ><font color="#ff0000"   >注：此步完成后，请执行以下命令，用于确定你的<span lang="en-US"   >tf</span>卡是否兼容<span lang="en-US"   >linux</span>的分区软件。</font></p>
<p style="text-indent: 0.74cm; margin-bottom: 0cm;"   ><span lang="en-US"   >#<font color="#ff0000"   >
fdisk -l /dev/mmcblk0</font></span></p>
<p style="text-indent: 0.74cm; margin-bottom: 0cm;"   ><br>
</p>
<p style="text-indent: 0.74cm; margin-bottom: 0cm;"   ><span lang="en-US"   >Disk
/dev/mmcblk0: 15.9 GB, 15931539456 bytes</span></p>
<p style="text-indent: 0.74cm; margin-bottom: 0cm;"   ><span lang="en-US"   >4
heads, 16 sectors/track, 486192 cylinders, total 31116288 sectors</span></p>
<p style="text-indent: 0.74cm; margin-bottom: 0cm;"   ><span lang="en-US"   >Units
= sectors of 1 * 512 = 512 bytes</span></p>
<p style="text-indent: 0.74cm; margin-bottom: 0cm;"   ><span lang="en-US"   >Sector
size (logical/physical): 512 bytes / 512 bytes</span></p>
<p style="text-indent: 0.74cm; margin-bottom: 0cm;"   ><span lang="en-US"   >I/O
size (minimum/optimal): 512 bytes / 512 bytes</span></p>
<p style="text-indent: 0.74cm; margin-bottom: 0cm;"   ><span lang="en-US"   >Disk
identifier: 0x00000000</span></p>
<p style="text-indent: 0.74cm; margin-bottom: 0cm;"   ><br>
</p>
<p style="text-indent: 0.74cm; margin-bottom: 0cm;"   >        <span lang="en-US"   >Device
Boot      Start         End      Blocks   Id  System</span></p>
<p style="text-indent: 0.74cm; margin-bottom: 0cm;"   ><span lang="en-US"   >/dev/mmcblk0p1
           <font color="#ff0000"   >2048</font>       34815       16384 
  c  W95 FAT32 (LBA)</span></p>
<p style="text-indent: 0.74cm; margin-bottom: 0cm;"   ><span lang="en-US"   >/dev/mmcblk0p2
          34816    31116287    15540736   83  Linux</span></p>
<p style="text-indent: 0.74cm; margin-bottom: 0cm;"   ><br>
</p>
<p style="text-indent: 0.74cm; margin-bottom: 0cm;"   ><font color="#ff0000"   >注：请注意上面第一个分区，红色的<span lang="en-US"   >2048</span>，如果此处值不为<span lang="en-US"   >2048</span>，说明<span lang="en-US"   >linux</span>对你的卡不兼容，不支持这种制引导区方式。目前已知一种杂牌只有类似<span lang="en-US"   >SD-C02G
TAIWAN</span>的卡不支持（移动送的，好东西，也不送你）。</font></p>
<p style="text-indent: 0.74cm; margin-bottom: 0cm;"   ><font color="#ff0000"   >解决办法如下：</font></p>
<p align="JUSTIFY"   style="margin-left: 0.74cm; text-indent: 0.71cm; margin-bottom: 0cm; line-height: 100%; page-break-inside: auto; widows: 0; orphans: 0; page-break-before: auto; page-break-after: auto;"   >
<font color="#ff0000"   >使用<span lang="en-US"   >berryboot-cubieboard</span>等<span lang="en-US"   >img</span>文件在<span lang="en-US"   >windows</span>下刷到<span lang="en-US"   >TF</span>卡，安装系统完成后。拿到<span lang="en-US"   >linux</span>下接着往下执行，相当于使用已经分区的卡进行安装。如果哪位对这种无法识别的卡有更好的方法，请告诉我。</font></p>
<p style="text-indent: 0.74cm; margin-bottom: 0cm;"   ><br>
</p>
<p style="text-indent: 0.74cm; margin-bottom: 0cm;"   ><br>
</p>
<p style="text-indent: 0.74cm; margin-bottom: 0cm;"   >将第一分区格式化成<span lang="en-US"   >vfat</span>格式</p>
<p style="text-indent: 0.74cm; margin-bottom: 0cm;"   ><span lang="en-US"   >#
<font color="#000080"   >mkfs.vfat /dev/mmcblk0p1</font> </span>
</p>
<p style="text-indent: 0.74cm; margin-bottom: 0cm;"   ><span lang="en-US"   >mkfs.vfat
3.0.13 (30 Jun 2012)</span></p>
<p style="text-indent: 0.74cm; margin-bottom: 0cm;"   ><br>
</p>
<p style="text-indent: 0.74cm; margin-bottom: 0cm;"   >将第二分区格式化成<span lang="en-US"   >ext4</span>格式，看你的卡的容量，可能要稍等一会儿。</p>
<p style="text-indent: 0.74cm; margin-bottom: 0cm;"   ><span lang="en-US"   >#
<font color="#000080"   >mkfs.ext4 /dev/mmcblk0p2</font> </span>
</p>
<p style="text-indent: 0.74cm; margin-bottom: 0cm;"   ><span lang="en-US"   >mke2fs
1.42.5 (29-Jul-2012)</span></p>
<p style="text-indent: 0.74cm; margin-bottom: 0cm;"   ><span lang="en-US"   >Discarding
device blocks: </span>完成<font face="Times New Roman, Liberation Serif"   >
                           </font>
</p>
<p style="text-indent: 0.74cm; margin-bottom: 0cm;"   >文件系统标签<span lang="en-US"   >=</span></p>
<p style="text-indent: 0.74cm; margin-bottom: 0cm;"   ><span lang="en-US"   >OS
type: Linux</span></p>
<p style="text-indent: 0.74cm; margin-bottom: 0cm;"   >块大小<span lang="en-US"   >=4096
(log=2)</span></p>
<p style="text-indent: 0.74cm; margin-bottom: 0cm;"   >分块大小<span lang="en-US"   >=4096
(log=2)</span></p>
<p style="text-indent: 0.74cm; margin-bottom: 0cm;"   ><span lang="en-US"   >Stride=0
blocks, Stripe width=0 blocks</span></p>
<p style="text-indent: 0.74cm; margin-bottom: 0cm;"   ><span lang="en-US"   >972944
inodes, 3885184 blocks</span></p>
<p style="text-indent: 0.74cm; margin-bottom: 0cm;"   ><span lang="en-US"   >194259
blocks (5.00%) reserved for the super user</span></p>
<p style="text-indent: 0.74cm; margin-bottom: 0cm;"   >第一个数据块<span lang="en-US"   >=0</span></p>
<p style="text-indent: 0.74cm; margin-bottom: 0cm;"   ><span lang="en-US"   >Maximum
filesystem blocks=3980394496</span></p>
<p style="text-indent: 0.74cm; margin-bottom: 0cm;"   ><span lang="en-US"   >119
block groups</span></p>
<p style="text-indent: 0.74cm; margin-bottom: 0cm;"   ><span lang="en-US"   >32768
blocks per group, 32768 fragments per group</span></p>
<p style="text-indent: 0.74cm; margin-bottom: 0cm;"   ><span lang="en-US"   >8176
inodes per group</span></p>
<p style="text-indent: 0.74cm; margin-bottom: 0cm;"   ><span lang="en-US"   >Superblock
backups stored on blocks: </span>
</p>
<p style="text-indent: 0.74cm; margin-bottom: 0cm;"   ><span lang="en-US"   >	32768,
98304, 163840, 229376, 294912, 819200, 884736, 1605632, 2654208</span></p>
<p style="text-indent: 0.74cm; margin-bottom: 0cm;"   ><br>
</p>
<p style="text-indent: 0.74cm; margin-bottom: 0cm;"   ><span lang="en-US"   >Allocating
group tables: </span>完成<font face="Times New Roman, Liberation Serif"   >
                           </font>
</p>
<p style="text-indent: 0.74cm; margin-bottom: 0cm;"   >正在写入<span lang="en-US"   >inode</span>表<span lang="en-US"   >:
</span>完成<font face="Times New Roman, Liberation Serif"   >         
                  </font>
</p>
<p style="text-indent: 0.74cm; margin-bottom: 0cm;"   ><span lang="en-US"   >Creating
journal (32768 blocks): </span>完成</p>
<p style="text-indent: 0.74cm; margin-bottom: 0cm;"   ><span lang="en-US"   >Writing
superblocks and filesystem accounting information: </span>完成<font face="Times New Roman, Liberation Serif"   >
 </font>
</p>
<p style="margin-bottom: 0cm;"   ><br>
</p>
<ol start="3"   >
	<li><p style="margin-bottom: 0cm;"   ><b>建立引导</b></p>
</li></ol>
<p align="JUSTIFY"   style="text-indent: 0.74cm; margin-bottom: 0cm; widows: 0; orphans: 0;"   >
<span lang="en-US"   ># <font color="#000080"   >git clone
</font><font color="#0000ff"   ><a rel="nofollow" href="https://github.com/linux-sunxi/u-boot-sunxi.git"   >https://github.com/linux-sunxi/u-boot-sunxi.git</a></font><font color="#000080"   >§</font></span></p>
<p align="JUSTIFY"   style="text-indent: 0.74cm; margin-bottom: 0cm; widows: 0; orphans: 0;"   >
<span lang="en-US"   ># <font color="#000080"   >cd u-boot-sunxi/</font></span></p>
<p align="JUSTIFY"   style="text-indent: 0.74cm; margin-bottom: 0cm; widows: 0; orphans: 0;"   >
<span lang="en-US"   ># <font color="#000080"   >make distclean
CROSS_COMPILE=arm-linux-gnueabihf-</font></span></p>
<p style="margin-left: 0.71cm; margin-bottom: 0cm;"   ><span lang="en-US"   >#
<font color="#000080"   >make cubieboard
CROSS_COMPILE=arm-linux-gnueabihf-</font></span></p>
<p style="margin-left: 0.71cm; margin-bottom: 0cm;"   >…………</p>
<p style="margin-left: 0.71cm; margin-bottom: 0cm;"   >…………</p>
<p style="margin-left: 0.71cm; margin-bottom: 0cm;"   ><span lang="en-US"   >arm-linux-gnueabihf-objcopy
-O srec hello_world hello_world.srec 2&gt;/dev/null</span></p>
<p style="margin-left: 0.71cm; margin-bottom: 0cm;"   ><span lang="en-US"   >arm-linux-gnueabihf-objcopy
-O binary hello_world hello_world.bin 2&gt;/dev/null</span></p>
<p style="margin-left: 0.71cm; margin-bottom: 0cm;"   ><span lang="en-US"   >make[2]:</span>正在离开目录<font face="Times New Roman, Liberation Serif"   >
</font><span lang="en-US"   >`/root/cubieboard/u-boot-sunxi/examples/standalone'</span></p>
<p style="margin-left: 0.71cm; margin-bottom: 0cm;"   ><span lang="en-US"   >make
-C examples/api all</span></p>
<p style="margin-left: 0.71cm; margin-bottom: 0cm;"   ><span lang="en-US"   >make[2]:
</span>正在进入目录<font face="Times New Roman, Liberation Serif"   >
</font><span lang="en-US"   >`/root/cubieboard/u-boot-sunxi/examples/api'</span></p>
<p style="margin-left: 0.71cm; margin-bottom: 0cm;"   ><span lang="en-US"   >make[2]:
</span>没有什么可以做的为<font face="Times New Roman, Liberation Serif"   >
</font><span lang="en-US"   >`all'</span>。</p>
<p style="margin-left: 0.71cm; margin-bottom: 0cm;"   ><span lang="en-US"   >make[2]:</span>正在离开目录<font face="Times New Roman, Liberation Serif"   >
</font><span lang="en-US"   >`/root/cubieboard/u-boot-sunxi/examples/api'</span></p>
<p style="margin-left: 0.71cm; margin-bottom: 0cm;"   ><span lang="en-US"   >make[1]:</span>正在离开目录<font face="Times New Roman, Liberation Serif"   >
</font><span lang="en-US"   >`/root/cubieboard/u-boot-sunxi'</span></p>
<p style="margin-left: 0.71cm; margin-bottom: 0cm;"   ><br>
</p>
<p style="margin-left: 0.71cm; margin-bottom: 0cm;"   ><span lang="en-US"   >#
<font color="#000080"   >dd if=spl/sunxi-spl.bin of=/dev/mmcblk0 bs=1024
seek=8</font></span></p>
<p style="margin-left: 0.71cm; margin-bottom: 0cm;"   >记录了<span lang="en-US"   >20+0
</span>的读入</p>
<p style="margin-left: 0.71cm; margin-bottom: 0cm;"   >记录了<span lang="en-US"   >20+0
</span>的写出</p>
<p style="margin-left: 0.71cm; margin-bottom: 0cm;"   ><span lang="en-US"   >20480</span>字节<span lang="en-US"   >(20
kB)</span>已复制，<span lang="en-US"   >0.0129492 </span>秒，<span lang="en-US"   >1.6
MB/</span>秒</p>
<p style="margin-left: 0.71cm; margin-bottom: 0cm;"   ><br>
</p>
<p style="margin-left: 0.71cm; margin-bottom: 0cm;"   ><span lang="en-US"   >#
<font color="#000080"   >dd if=u-boot.bin of=/dev/mmcblk0 bs=1024
seek=32</font></span></p>
<p style="margin-left: 0.71cm; margin-bottom: 0cm;"   >记录了<span lang="en-US"   >168+1
</span>的读入</p>
<p style="margin-left: 0.71cm; margin-bottom: 0cm;"   >记录了<span lang="en-US"   >168+1
</span>的写出</p>
<p style="margin-left: 0.71cm; margin-bottom: 0cm;"   ><span lang="en-US"   >172976</span>字节<span lang="en-US"   >(173
kB)</span>已复制，<span lang="en-US"   >0.0515786 </span>秒，<span lang="en-US"   >3.4
MB/</span>秒</p>
<p style="margin-left: 0.71cm; margin-bottom: 0cm;"   ><br>
</p>
<p style="margin-left: 0.71cm; margin-bottom: 0cm;"   ><span lang="en-US"   >#
<font color="#000080"   >cd ..</font></span></p>
<p style="margin-left: 0.71cm; margin-bottom: 0cm;"   ><br>
</p>
<ol start="4"   >
	<li><p style="margin-bottom: 0cm;"   ><b>编译内核</b></p>
</li></ol>
<p style="text-indent: 0.74cm; margin-bottom: 0cm;"   >
下载内核源码，如果通过<span lang="en-US"   >git</span>下载可能时间较长。</p>
<p style="text-indent: 0.74cm; margin-bottom: 0cm;"   ><span lang="en-US"   >#
<font color="#000080"   >git clone
git://github.com/linux-sunxi/linux-sunxi.git</font></span></p>
<p style="text-indent: 0.74cm; margin-bottom: 0cm;"   ><span lang="en-US"   >#
<font color="#000080"   >cd linux-sunxi/</font></span></p><p style="text-indent: 0px; margin-bottom: 0cm;"   ><font color="#333333"   >　　检查内核源码树，是否纯净。不纯净，则会CLEAN。</font></p><p style="text-indent: 0.74cm; margin-bottom: 0cm;"   ><span lang="en-US"   ><span style="line-height: 22px;"   >#&nbsp;</span><font color="#000080"   style="line-height: 22px;"   >make ARCH=arm mrproper</font></span></p>
<p style="text-indent: 0.74cm; margin-bottom: 0cm;"   >使用<span lang="en-US"   >sun4i</span>的默认配置（<font color="#ff0000"   >第一次编译时使用</font>）<br></p>
<p style="text-indent: 0.74cm; margin-bottom: 0cm;"   ><span lang="en-US"   >#
<font color="#000080"   >make ARCH=arm sun4i_defconfig</font></span></p>
<p style="text-indent: 0.74cm; margin-bottom: 0cm;"   ><span lang="en-US"   >#</span></p>
<p style="text-indent: 0.74cm; margin-bottom: 0cm;"   ><span lang="en-US"   >#
configuration written to .config</span></p>
<p style="text-indent: 0.74cm; margin-bottom: 0cm;"   ><span lang="en-US"   >#</span></p>
<p style="text-indent: 0.74cm; margin-bottom: 0cm;"   ><br>
</p>
<p style="text-indent: 0.74cm; margin-bottom: 0cm;"   ><span lang="en-US"   >;</span><font color="#000000"   >读取老的配置文件（</font><font color="#ff0000"   >非第一次编译时使用，用于更改内核配置</font><font color="#000000"   >）</font></p>
<p style="margin-left: 0.71cm; margin-bottom: 0cm;"   ><span lang="en-US"   >#
<font color="#000080"   >make ARCH=arm oldconfig</font></span></p>
<p style="margin-left: 0.71cm; margin-bottom: 0cm;"   ><span lang="en-US"   >scripts/kconfig/conf
--oldconfig Kconfig</span></p>
<p style="margin-left: 0.71cm; margin-bottom: 0cm;"   ><span lang="en-US"   >#</span></p>
<p style="margin-left: 0.71cm; margin-bottom: 0cm;"   ><span lang="en-US"   >#
configuration written to .config</span></p>
<p style="margin-left: 0.71cm; margin-bottom: 0cm;"   ><span lang="en-US"   >#</span></p>
<p style="margin-left: 0.71cm; margin-bottom: 0cm;"   ><br>
</p>
<p style="margin-left: 0.71cm; margin-bottom: 0cm;"   >选择内核编译配置（根据个自的情况而定，选择完成后<font color="#ff0000"   >保存</font>）</p>
<p style="margin-left: 0.71cm; margin-bottom: 0cm;"   ><span lang="en-US"   >#
<font color="#000080"   >make ARCH=arm menuconfig</font></span></p>
<p style="margin-left: 0.71cm; margin-bottom: 0cm;"   ><span lang="en-US"   >scripts/kconfig/mconf
Kconfig</span></p>
<p style="margin-left: 0.71cm; margin-bottom: 0cm;"   ><span lang="en-US"   >#</span></p>
<p style="margin-left: 0.71cm; margin-bottom: 0cm;"   ><span lang="en-US"   >#
configuration written to .config</span></p>
<p style="margin-left: 0.71cm; margin-bottom: 0cm;"   ><span lang="en-US"   >#</span></p>
<p style="margin-left: 0.71cm; margin-bottom: 0cm;"   ><br>
</p>
<p style="margin-left: 0.71cm; margin-bottom: 0cm;"   ><br>
</p>
<p style="margin-left: 0.71cm; margin-bottom: 0cm;"   ><span lang="en-US"   >***
End of the configuration.</span></p>
<p style="margin-left: 0.71cm; margin-bottom: 0cm;"   ><span lang="en-US"   >***
Execute 'make' to start the build or try 'make help'.</span></p>
<p style="margin-left: 0.71cm; margin-bottom: 0cm;"   ><br>
</p>
<p style="margin-left: 0.71cm; margin-bottom: 0cm;"   >编译内核，时间较长，请耐心等待</p>
<p style="margin-left: 0.71cm; margin-bottom: 0cm;"   ><span lang="en-US"   >#<font color="#000080"   >
make ARCH=arm CROSS_COMPILE=arm-linux-gnueabihf- uImage</font> </span>
</p>
<p style="margin-left: 0.71cm; margin-bottom: 0cm;"   ><span lang="en-US"   >scripts/kconfig/conf
--silentoldconfig Kconfig</span></p>
<p style="margin-left: 0.71cm; margin-bottom: 0cm;"   >
………………</p>
<p style="margin-left: 0.71cm; margin-bottom: 0cm;"   >
………………</p>
<p style="margin-left: 0.71cm; margin-bottom: 0cm;"   ><span lang="en-US"   >Image
Name:   Linux-3.0.62+</span></p>
<p style="margin-left: 0.71cm; margin-bottom: 0cm;"   ><span lang="en-US"   >Created:
     Thu Feb 14 23:10:48 2013</span></p>
<p style="margin-left: 0.71cm; margin-bottom: 0cm;"   ><span lang="en-US"   >Image
Type:   ARM Linux Kernel Image (uncompressed)</span></p>
<p style="margin-left: 0.71cm; margin-bottom: 0cm;"   ><span lang="en-US"   >Data
Size:    4106068 Bytes = 4009.83 kB = 3.92 MB</span></p>
<p style="margin-left: 0.71cm; margin-bottom: 0cm;"   ><span lang="en-US"   >Load
Address: 40008000</span></p>
<p style="margin-left: 0.71cm; margin-bottom: 0cm;"   ><span lang="en-US"   >Entry
Point:  40008000</span></p>
<p style="margin-left: 0.71cm; margin-bottom: 0cm;"   >  <span lang="en-US"   >Image
arch/arm/boot/uImage is ready</span></p>
<p align="JUSTIFY"   style="margin-left: 0.71cm; margin-bottom: 0cm; line-height: 100%; page-break-inside: auto; widows: 0; orphans: 0; page-break-before: auto; page-break-after: auto;"   >
<font color="#ff0000"   >注：请确认编译无误。正确应该看到<span lang="en-US"   >Image
arch/arm/boot/uImage is ready</span></font><font color="#ff0000"   >。否则请根据提示再执行<span lang="en-US"   >#
</span></font><font color="#000080"   >make ARCH=arm menuconfig</font><font color="#ff0000"   >
; # </font><font color="#000080"   >make ARCH=arm
CROSS_COMPILE=arm-linux-gnueabihf- uImage</font>
<font color="#ff0000"   >直至正确。一些选项可能造成编译无法编译通过，可以如果不是重要功能可以取消或与维护者联系。</font></p>
<p style="margin-left: 0.71cm; margin-bottom: 0cm;"   ><br>
</p>
<p style="margin-left: 0.71cm; margin-bottom: 0cm;"   ><span lang="en-US"   >#
<font color="#000080"   >make ARCH=arm
CROSS_COMPILE=arm-linux-gnueabihf- modules</font></span></p>
<p style="margin-left: 0.71cm; margin-bottom: 0cm;"   >  <span lang="en-US"   >CHK
    include/linux/version.h</span></p>
<p style="margin-left: 0.71cm; margin-bottom: 0cm;"   >
………………</p>
<p style="margin-left: 0.71cm; margin-bottom: 0cm;"   >
………………</p>
<p style="margin-left: 0.71cm; margin-bottom: 0cm;"   ><span lang="en-US"   >LD
[M]  net/ipv6/xfrm6_mode_tunnel.ko </span>
</p>
<p style="margin-left: 0.71cm; margin-bottom: 0cm;"   ><font color="#ff0000"   >注：以上结果，因每个人选择不同结果不同，只是举例，请勿以此为结果。</font></p>
<p align="JUSTIFY"   style="margin-left: 0.71cm; margin-bottom: 0cm; line-height: 100%; page-break-inside: auto; widows: 0; orphans: 0; page-break-before: auto; page-break-after: auto;"   >
<font color="#ff0000"   >请确保编译无误，正确应该看到类似</font><span lang="en-US"   >LD
[M] XXXX/XXXX/XXX.ko</span><font color="#ff0000"   >。否则请根据提示再执行<span lang="en-US"   >#
</span></font><font color="#000080"   >make ARCH=arm menuconfig</font><font color="#ff0000"   >
; # </font><font color="#000080"   >make ARCH=arm
CROSS_COMPILE=arm-linux-gnueabihf- uImage</font> <font color="#ff0000"   >;
#</font> <font color="#000080"   >make ARCH=arm
CROSS_COMPILE=arm-linux-gnueabihf-
modules</font><font color="#ff0000"   >直至正确。一些选项可能造成编译无法编译通过，可以如果不是重要功能可以取消或与维护者联系。</font></p>
<p style="margin-left: 0.71cm; margin-bottom: 0cm;"   >
<br>
</p>
<p style="margin-left: 0.71cm; margin-bottom: 0cm;"   ><span lang="en-US"   >#
<font color="#000080"   >cd ..</font></span></p>
<p style="margin-left: 0.71cm; margin-bottom: 0cm;"   ><br>
</p>
<ol start="5"   >
	<li><p style="margin-bottom: 0cm;"   ><b>制做</b><span lang="en-US"   ><b>script.bin</b></span></p>
</li></ol>
<p style="margin-left: 0.71cm; margin-bottom: 0cm;"   ><span lang="en-US"   >#
<font color="#000080"   >git clone
</font><font color="#0000ff"   ><a rel="nofollow" href="https://github.com/linux-sunxi/sunxi-tools.git"   >https://github.com/linux-sunxi/sunxi-tools.git</a></font><font color="#000080"   >§</font></span></p><p style="margin-left: 0.71cm; margin-bottom: 0cm;"   ><span lang="en-US"   ><font color="#000080"   ># cd sunxi-tools</font></span></p>
<p style="margin-left: 0.71cm; margin-bottom: 0cm;"   ><span lang="en-US"   >#
<font color="#000080"   >make</font></span></p>
<p style="margin-left: 0.71cm; margin-bottom: 0cm;"   ><span lang="en-US"   >gcc
-g -O0 -Wall -Wextra -std=c99 -D_POSIX_C_SOURCE=200112L -Iinclude/ 
-o fexc fexc.c script.c script_uboot.c script_bin.c script_fex.c </span>
</p>
<p style="margin-left: 0.71cm; margin-bottom: 0cm;"   ><span lang="en-US"   >ln
-s fexc bin2fex</span></p>
<p style="margin-left: 0.71cm; margin-bottom: 0cm;"   ><span lang="en-US"   >ln
-s fexc fex2bin</span></p>
<p style="margin-left: 0.71cm; margin-bottom: 0cm;"   ><span lang="en-US"   >gcc
-g -O0 -Wall -Wextra -std=c99 -D_POSIX_C_SOURCE=200112L -Iinclude/ 
-o bootinfo bootinfo.c </span>
</p>
<p style="margin-left: 0.71cm; margin-bottom: 0cm;"   ><span lang="en-US"   >bootinfo.c:
</span>在函数‘<span lang="en-US"   >print_script<font face="宋体, 方正书宋_GBK"   >’</font></span>中<span lang="en-US"   >:</span></p>
<p style="margin-left: 0.71cm; margin-bottom: 0cm;"   ><span lang="en-US"   >bootinfo.c:274:25:
</span>警告：<font face="Times New Roman, Liberation Serif"   >
</font>未使用的参数‘<span lang="en-US"   >script<font face="宋体, 方正书宋_GBK"   >’</font>
[-Wunused-parameter]</span></p>
<p style="margin-left: 0.71cm; margin-bottom: 0cm;"   ><span lang="en-US"   >gcc
-g -O0 -Wall -Wextra -std=c99 -D_POSIX_C_SOURCE=200112L -Iinclude/
`pkg-config --cflags libusb-1.0`  -o fel fel.c  `pkg-config --libs
libusb-1.0`</span></p>
<p style="margin-left: 0.71cm; margin-bottom: 0cm;"   ><span lang="en-US"   >gcc
-g -O0 -Wall -Wextra -std=c99 -D_POSIX_C_SOURCE=200112L -Iinclude/ 
-o pio pio.c </span>
</p>
<p style="margin-left: 0.71cm; margin-bottom: 0cm;"   ><span lang="en-US"   >pio.c:
</span>在函数‘<span lang="en-US"   >do_command<font face="宋体, 方正书宋_GBK"   >’</font></span>中<span lang="en-US"   >:</span></p>
<p style="margin-left: 0.71cm; margin-bottom: 0cm;"   ><span lang="en-US"   >pio.c:313:57:
</span>警告：<font face="Times New Roman, Liberation Serif"   >
</font>未使用的参数‘<span lang="en-US"   >argc<font face="宋体, 方正书宋_GBK"   >’</font>
[-Wunused-parameter]</span></p>
<p style="margin-left: 0.71cm; margin-bottom: 0cm;"   ><span lang="en-US"   >gcc
-g -O0 -Wall -Wextra -std=c99 -D_POSIX_C_SOURCE=200112L -Iinclude/ 
-o nand-part nand-part.c</span></p>
<p style="margin-left: 0.71cm; margin-bottom: 0cm;"   ><br>
</p>
<p style="margin-left: 0.71cm; margin-bottom: 0cm;"   >得到<font face="Times New Roman, Liberation Serif"   >
</font><span lang="en-US"   >fex2bin </span>文件，这个是能把<font face="Times New Roman, Liberation Serif"   >
</font><span lang="en-US"   >*.fex </span>文件生成<font face="Times New Roman, Liberation Serif"   >
</font><span lang="en-US"   >*.bin</span>文件。</p>
<p style="margin-left: 0.71cm; margin-bottom: 0cm;"   ><span lang="en-US"   >#
<font color="#000080"   >cd ..</font></span></p>
<p style="margin-bottom: 0cm;"   ><br>
</p>
<p style="margin-left: 0.71cm; margin-bottom: 0cm;"   ><span lang="en-US"   >#
<font color="#000080"   >git clone
</font><font color="#0000ff"   ><a rel="nofollow" href="https://github.com/linux-sunxi/sunxi-boards.git"   >https://github.com/linux-sunxi/sunxi-boards.git</a></font><font color="#000080"   >§</font></span></p>
<p style="margin-left: 0.71cm; margin-bottom: 0cm;"   ><span lang="en-US"   >#
<font color="#000080"   >cd sunxi-boards/sys_config/a10/</font></span></p>
<p style="margin-left: 0.71cm; margin-bottom: 0cm;"   ><br>
</p>
<p style="margin-left: 0.71cm; margin-bottom: 0cm;"   >在<font face="Times New Roman, Liberation Serif"   >
</font><span lang="en-US"   >sys_config/a10 </span>目录下，我们能找到<font face="Times New Roman, Liberation Serif"   >
</font><span lang="en-US"   >cubieboard.fex </span>文件，这就是我们需要的</p>
<p style="margin-left: 0.71cm; margin-bottom: 0cm;"   >编译，得到<font face="Times New Roman, Liberation Serif"   >
</font><span lang="en-US"   >script.bin</span></p>
<p style="margin-left: 0.71cm; margin-bottom: 0cm;"   ><br>
</p>
<p style="margin-left: 0.71cm; margin-bottom: 0cm;"   ><span lang="en-US"   >#
<font color="#000080"   >../../../sunxi-tools/fex2bin cubieboard.fex
script.bin</font></span></p>
<p style="margin-bottom: 0cm;"   ><br>
</p>
<ol start="6"   >
	<li><p style="margin-bottom: 0cm;"   ><b>建立引导</b></p>
</li></ol>
<p style="text-indent: 0.74cm; margin-bottom: 0cm;"   >建立引导区挂载点（<font color="#ff0000"   >注，此时应在<span lang="en-US"   >a10#</span></font><font color="#ff0000"   >目录下，主要为了拷贝方便</font>）</p>
<p style="margin-left: 0.71cm; margin-bottom: 0cm;"   ><span lang="en-US"   >#
<font color="#000080"   >mkdir -p /mnt/1</font></span></p>
<p style="margin-left: 0.71cm; margin-bottom: 0cm;"   ><span lang="en-US"   >#
<font color="#000080"   >mkdir -p /mnt/2</font></span></p>
<p style="margin-left: 0.71cm; margin-bottom: 0cm;"   ><span lang="en-US"   >#
<font color="#000080"   >mount /dev/mmcblk0p1 /mnt/1</font></span></p>
<p style="margin-left: 0.71cm; margin-bottom: 0cm;"   ><span lang="en-US"   >#
<font color="#000080"   >mount /dev/mmcblk0p2 /mnt/2</font></span></p>
<p style="margin-left: 0.71cm; margin-bottom: 0cm;"   ><br>
</p>
<p style="margin-left: 0.71cm; margin-bottom: 0cm;"   ><span lang="en-US"   >#
<font color="#000080"   >cp script.bin /mnt/1/</font></span></p>
<p style="margin-left: 0.71cm; margin-bottom: 0cm;"   ><br>
</p>
<p style="margin-left: 0.71cm; margin-bottom: 0cm;"   >进入内核目录</p>
<p style="margin-left: 0.71cm; margin-bottom: 0cm;"   ><span lang="en-US"   >#
<font color="#000080"   >cd ../../../linux-sunxi/</font></span></p>
<p style="margin-left: 0.71cm; margin-bottom: 0cm;"   ><span lang="en-US"   >#
<font color="#000080"   >cp arch/arm/boot/uImage /mnt/1/</font></span></p>
<p style="margin-bottom: 0cm;"   ><br>
</p>
<ol start="7"   >
	<li><p style="margin-bottom: 0cm;"   ><b>建立</b><span lang="en-US"   ><b>rootfs</b></span></p>
</li></ol>
<p style="text-indent: 0.74cm; margin-bottom: 0cm;"   >此处，是本人遇到的最大的麻烦。由于没有看清楚是<span lang="en-US"   >ubuntu</span>还是<span lang="en-US"   >debain,</span>导致死活无法引导，<span lang="en-US"   >ubuntu</span>的<span lang="en-US"   >rootfs</span>，引导时<span lang="en-US"   >inittab</span>已经不默认引导，安装时默认也无此文件，两者安装是有区别的。如果在<span lang="en-US"   >ubuntu</span>下直接使用<span lang="en-US"   >inittab</span>会循环出现如下信息：</p>
<p style="text-indent: 0.74cm; margin-bottom: 0cm;"   ><span lang="en-US"   >&lt;3&gt;init:
Failed to create pty - disabling logging for job</span></p>
<p style="text-indent: 0.74cm; margin-bottom: 0cm;"   ><span lang="en-US"   >[
   5.140000] init: Failed to create pty - disabling logging for job</span></p>
<p style="text-indent: 0.74cm; margin-bottom: 0cm;"   ><span lang="en-US"   >&lt;4&gt;init:
Temporary process spawn error: No such file or directory</span></p>
<p style="text-indent: 0.74cm; margin-bottom: 0cm;"   ><span lang="en-US"   >[
   5.150000] init: Temporary process spawn error: No such file or
directory</span></p>
<p style="text-indent: 0.74cm; margin-bottom: 0cm;"   ><br>
</p>
<p style="text-indent: 0.74cm; margin-bottom: 0cm;"   >有兴趣的朋友可以试一下。研究出来，可以告诉我一下，谢谢。</p>
<p style="text-indent: 0.74cm; margin-bottom: 0cm;"   ><span lang="en-US"   >##
debootstrap --arch=armhf --variant=buildd --foreign precise /mnt/</span></p>
<p style="text-indent: 0.74cm; margin-bottom: 0cm;"   ><br>
</p>
<p style="text-indent: 0.74cm; margin-bottom: 0cm;"   >以下是我找的一个国内的<span lang="en-US"   >debian
arm</span>的国内源，发现国内的一些源并不提供<span lang="en-US"   >arm</span>的源。即使如此，也是需要一点时间的，耐心等吧。</p>
<p style="text-indent: 0.74cm; margin-bottom: 0cm;"   ><br>
</p>
<p align="JUSTIFY"   style="margin-left: 0.71cm; margin-bottom: 0cm; line-height: 100%; page-break-inside: auto; widows: 0; orphans: 0; page-break-before: auto; page-break-after: auto;"   >
<span lang="en-US"   ># <font color="#000080"   >debootstrap --arch=armhf
--variant=buildd --foreign wheezy /mnt/2/
http://ftp.cn.debian.org/debian</font></span></p>
<p style="text-indent: 0.74cm; margin-bottom: 0cm;"   >………………</p>
<p style="text-indent: 0.74cm; margin-bottom: 0cm;"   >………………</p>
<p style="margin-left: 0.71cm; margin-bottom: 0cm;"   ><span lang="en-US"   >I:
Extracting liblzma5...</span></p>
<p style="margin-left: 0.71cm; margin-bottom: 0cm;"   ><span lang="en-US"   >I:
Extracting xz-utils...</span></p>
<p style="margin-left: 0.71cm; margin-bottom: 0cm;"   ><span lang="en-US"   >I:
Extracting zlib1g...</span></p>
<p style="margin-left: 0.71cm; margin-bottom: 0cm;"   ><br>
</p>
<p style="margin-left: 0.71cm; margin-bottom: 0cm;"   ><span lang="en-US"   >#
<font color="#000000"   >ls /mnt/2</font></span></p>
<p style="margin-left: 0.71cm; margin-bottom: 0cm;"   ><span lang="en-US"   >bin
  debootstrap  etc   lib         mnt   root  sbin     sys  usr</span></p>
<p style="margin-left: 0.71cm; margin-bottom: 0cm;"   ><span lang="en-US"   >boot
 dev          home  lost+found  proc  run   selinux  tmp  var</span></p>
<p style="margin-left: 0.71cm; margin-bottom: 0cm;"   >以上是你<span lang="en-US"   >rootfs</span>中的基本文件。如果还觉得大，请自行处理。</p>
<p style="margin-left: 0.71cm; margin-bottom: 0cm;"   ><br>
</p>
<p style="margin-left: 0.71cm; margin-bottom: 0cm;"   >拷贝<span lang="en-US"   >arm</span>的仿真环境</p>
<p style="margin-left: 0.71cm; margin-bottom: 0cm;"   ><span lang="en-US"   >#
<font color="#000080"   >cp /usr/bin/qemu-arm-static /mnt/2/usr/bin/</font></span></p>
<p style="margin-left: 0.71cm; margin-bottom: 0cm;"   ><span lang="en-US"   >#
<font color="#000080"   >chroot /mnt/2/</font></span></p>
<p style="margin-left: 0.71cm; margin-bottom: 0cm;"   ><font color="#000000"   >此时你将看到，你的提示符，前面已经加上</font><span lang="en-US"   >I
have no name!</span>。</p>
<p style="margin-left: 0.71cm; margin-bottom: 0cm;"   ><br>
</p>
<p style="margin-left: 0.71cm; margin-bottom: 0cm;"   >安装核心包</p>
<p style="margin-left: 0.71cm; margin-bottom: 0cm;"   ><span lang="en-US"   >#
<font color="#000080"   >/debootstrap/debootstrap --second-stage</font></span></p>
<p style="margin-left: 0.71cm; margin-bottom: 0cm;"   ><span lang="en-US"   >I:
Installing core packages...</span></p>
<p style="margin-left: 0.71cm; margin-bottom: 0cm;"   >………………</p>
<p style="margin-left: 0.71cm; margin-bottom: 0cm;"   >………………</p>
<p style="margin-left: 0.71cm; margin-bottom: 0cm;"   ><span lang="en-US"   >I:
Base system installed successfully.</span></p>
<p style="margin-left: 0.71cm; margin-bottom: 0cm;"   >这是啥，呵呵，你成功安装了最简系统。</p>
<p style="margin-left: 0.71cm; margin-bottom: 0cm;"   >接下来，可能是你容易忽略的一件事。更改你超级用户（<span lang="en-US"   >root</span>）的密码。</p>
<p style="margin-left: 0.71cm; margin-bottom: 0cm;"   ><span lang="en-US"   >#
chroot . passwd</span></p>
<p style="margin-left: 0.71cm; margin-bottom: 0cm;"   ><span lang="en-US"   >Enter
new UNIX password: </span>
</p>
<p style="margin-left: 0.71cm; margin-bottom: 0cm;"   ><span lang="en-US"   >Retype
new UNIX password: </span>
</p>
<p style="margin-left: 0.71cm; margin-bottom: 0cm;"   ><span lang="en-US"   >passwd:
password updated successfully</span></p>
<p style="margin-left: 0.71cm; margin-bottom: 0cm;"   >输入两遍一样的密码。方便的话能告诉我一下嘛。呵呵。。。</p>
<p style="margin-left: 0.71cm; margin-bottom: 0cm;"   ><span lang="en-US"   >#
<font color="#000080"   >exit</font></span></p>
<p style="margin-left: 0.71cm; margin-bottom: 0cm;"   >执行上面命令回到我们现实<span lang="en-US"   >PC</span>中。为什么呢。最小系统里工具比较少，折腾麻烦。而且我们还有工作没有做完。接着来。</p>
<p style="margin-left: 0.71cm; margin-bottom: 0cm;"   ><br>
</p>
<p style="margin-left: 0.71cm; margin-bottom: 0cm;"   >现在我们将安装系统的模块。在此之前，请确认你的目录。</p>
<p style="margin-left: 0.71cm; margin-bottom: 0cm;"   ><span lang="en-US"   >#
pwd</span></p>
<p style="margin-left: 0.71cm; margin-bottom: 0cm;"   ><span lang="en-US"   >/root/linux-sunxi</span></p>
<ol start="8"   >
	<li><p style="margin-bottom: 0cm;"   ><b>系统模块的安装</b></p>
</li></ol>
<p align="JUSTIFY"   style="text-indent: 0.74cm; margin-bottom: 0cm; line-height: 100%; page-break-inside: auto; widows: 0; orphans: 0; page-break-before: auto; page-break-after: auto;"   >
<span lang="en-US"   ># <font color="#000080"   >make ARCH=arm
CROSS_COMPILE=arm-linux-gnueabihf- INSTALL_MOD_PATH=/mnt/2/
modules_install</font></span></p>
<p style="text-indent: 0.74cm; margin-bottom: 0cm;"   >
………………</p>
<p style="text-indent: 0.74cm; margin-bottom: 0cm;"   >
………………</p>
<p style="margin-left: 0.71cm; margin-bottom: 0cm;"   > <span lang="en-US"   >DEPMOD
 3.0.62+</span></p>
<p style="margin-left: 0.71cm; margin-bottom: 0cm;"   ><br>
</p>
<p style="margin-left: 0.71cm; margin-bottom: 0cm;"   >
到此为止，你的系统，基本是安装完了。还需要最后一步。告诉系统，你的<span lang="en-US"   >rootfs</span>的位置。</p>
<p style="margin-left: 0.71cm; margin-bottom: 0cm;"   ><span lang="en-US"   >#
<font color="#000080"   >cd /mnt/1</font></span></p>
<p style="margin-left: 0.71cm; margin-bottom: 0cm;"   ><span lang="en-US"   >#
<font color="#000080"   >cat &lt;&lt;EOT &gt; boot.cmd</font></span></p>
<p style="margin-left: 0.71cm; margin-bottom: 0cm;"   ><span lang="en-US"   >&gt;
<font color="#000080"   >setenv bootargs console=ttyS0,115200
root=/dev/mmcblk0p2 rootwait panic=10 ${extra}</font></span></p>
<p style="margin-left: 0.71cm; margin-bottom: 0cm;"   ><span lang="en-US"   >&gt;
<font color="#000080"   >fatload mmc 0 0x43000000 script.bin</font></span></p>
<p style="margin-left: 0.71cm; margin-bottom: 0cm;"   ><span lang="en-US"   >&gt;
<font color="#000080"   >fatload mmc 0 0x48000000 uImage</font></span></p>
<p style="margin-left: 0.71cm; margin-bottom: 0cm;"   ><span lang="en-US"   >&gt;
<font color="#000080"   >bootm 0x48000000</font></span></p>
<p style="margin-left: 0.71cm; margin-bottom: 0cm;"   ><span lang="en-US"   >&gt;
<font color="#000080"   >EOT</font></span></p>
<p style="margin-left: 0.71cm; margin-bottom: 0cm;"   ><br>
</p>
<p style="margin-left: 0.71cm; margin-bottom: 0cm;"   ><span lang="en-US"   >#
<font color="#000080"   >mkimage -C none -A arm -T script -d boot.cmd
boot.scr</font></span></p>
<p style="margin-left: 0.71cm; margin-bottom: 0cm;"   ><span lang="en-US"   >Image
Name:   </span>
</p>
<p style="margin-left: 0.71cm; margin-bottom: 0cm;"   ><span lang="en-US"   >Created:
     Fri Feb 15 00:40:09 2013</span></p>
<p style="margin-left: 0.71cm; margin-bottom: 0cm;"   ><span lang="en-US"   >Image
Type:   ARM Linux Script (uncompressed)</span></p>
<p style="margin-left: 0.71cm; margin-bottom: 0cm;"   ><span lang="en-US"   >Data
Size:    169 Bytes = 0.17 kB = 0.00 MB</span></p>
<p style="margin-left: 0.71cm; margin-bottom: 0cm;"   ><span lang="en-US"   >Load
Address: 00000000</span></p>
<p style="margin-left: 0.71cm; margin-bottom: 0cm;"   ><span lang="en-US"   >Entry
Point:  00000000</span></p>
<p style="margin-left: 0.71cm; margin-bottom: 0cm;"   ><span lang="en-US"   >Contents:</span></p>
<p style="margin-left: 0.71cm; margin-bottom: 0cm;"   >   <span lang="en-US"   >Image
0: 161 Bytes = 0.16 kB = 0.00 MB</span></p>
<p style="margin-left: 0.71cm; margin-bottom: 0cm;"   ><br>
</p>
<ol start="9"   >
	<li><p style="margin-bottom: 0cm;"   ><b>编辑</b><span lang="en-US"   ><b>inittab</b></span><b>及</b><span lang="en-US"   ><b>fstab
	</b></span><b>文件</b></p>
</li></ol>
<p style="margin-left: 0.71cm; margin-bottom: 0cm;"   ><span lang="en-US"   >#
<font color="#000080"   >cd /mnt/2/etc/</font></span></p>
<p style="margin-left: 0.71cm; margin-bottom: 0cm;"   ><span lang="en-US"   >#
<font color="#000080"   >cat &lt;&lt;EOT &gt;&gt; inittab</font></span></p>
<p style="margin-left: 0.71cm; margin-bottom: 0cm;"   ><span lang="en-US"   >&gt;
<font color="#000080"   >T0:2345:respawn:/sbin/getty -L ttyS0 115200
linux</font></span></p>
<p style="margin-left: 0.71cm; margin-bottom: 0cm;"   ><span lang="en-US"   >&gt;
<font color="#000080"   >EOT</font></span></p>
<p style="margin-left: 0.71cm; margin-bottom: 0cm;"   ><br>
</p>
<p style="margin-left: 0.71cm; margin-bottom: 0cm;"   ><span lang="en-US"   >#
<font color="#000080"   >cat &lt;&lt;EOT &gt;&gt; fstab</font></span></p>
<p style="margin-left: 0.71cm; margin-bottom: 0cm;"   ><span lang="en-US"   >&gt;<font color="#000080"   >
proc            /proc           proc    defaults          0       0</font></span></p>
<p style="margin-left: 0.71cm; margin-bottom: 0cm;"   ><span lang="en-US"   >&gt;
<font color="#000080"   >/dev/mmcblk0p1  /boot           vfat   
defaults          0       2</font></span></p>
<p style="margin-left: 0.71cm; margin-bottom: 0cm;"   ><span lang="en-US"   >&gt;
<font color="#000080"   >/dev/mmcblk0p2  /               ext4   
defaults,noatime  0       1</font></span></p>
<p style="margin-left: 0.71cm; margin-bottom: 0cm;"   ><span lang="en-US"   >&gt;
<font color="#000080"   >EOT</font></span></p>
<p style="margin-bottom: 0cm;"   ><br>
</p>
<p style="margin-left: 0.71cm; margin-bottom: 0cm;"   ><span lang="en-US"   >OK</span>，整个系统制做完毕了。取卡。。。。</p>
<p style="margin-left: 0.71cm; margin-bottom: 0cm;"   ><br>
</p>
<p style="margin-left: 0.71cm; margin-bottom: 0cm;"   >再取卡前，请先执行以下命令。</p>
<p style="margin-left: 0.71cm; margin-bottom: 0cm;"   ><span lang="en-US"   >#
<font color="#000080"   >cd</font></span></p>
<p style="margin-left: 0.71cm; margin-bottom: 0cm;"   ><span lang="en-US"   >#
<font color="#000080"   >umount /mnt/1</font></span></p>
<p style="margin-left: 0.71cm; margin-bottom: 0cm;"   ><span lang="en-US"   >#
<font color="#000080"   >umount /mnt/2</font></span></p>
<p style="text-indent: 0.74cm; margin-bottom: 0cm;"   ><br>
</p>
<p style="text-indent: 0.74cm; margin-bottom: 0cm;"   >否则，你可能见到难见的黑屏。。。系统崩溃。。。</p>
<p style="text-indent: 0.74cm; margin-bottom: 0cm;"   >至此，全套终于打完。你可以把卡拨下来了。插到<span lang="en-US"   >cubieborad</span>上试试了。此方式安装也为没有<span lang="en-US"   >hdmi</span>接口显示器的用户安装系统带来了方便。可以直接用串口线连接，查看和执行。好人我就做到底吧，再把串连接也讲了吧。</p>
<p align="RIGHT"   style="text-indent: 0.74cm; margin-bottom: 0cm;"   ><font size="1"   style="font-size: 6pt;"   ><span lang="en-US"   ><font color="#0000ff"   ><a href="http://onefishum.blog.163.com/blog/static/5184730520131151385937/"   >http://onefishum.blog.163.com/blog/static/5184730520131151385937/</a></font></span></font></p>
<ol start="10"   >
	<li><p style="margin-bottom: 0cm;"   ><b>串口命令行执行</b></p>
</li></ol>
<p style="text-indent: 0.74cm; margin-bottom: 0cm;"   ><font color="#000000"   >首先将<span lang="en-US"   >cubieborad</span></font><font color="#000000"   >提供的串口线按如下方式，插在</font><span lang="en-US"   ><font color="#0000ff"   ><a href="http://onefishum.blog.163.com/blog/static/5184730520131151385937/"   >cubieborad</a></font><font color="#000000"   >§</font></span><font color="#000000"   >的<span lang="en-US"   >ttl</span></font><font color="#000000"   >接口上。</font></p>
<p style="text-indent: 0.74cm; margin-bottom: 0cm;"   >黑色 接板子上的
<span lang="en-US"   >GND </span>（地）</p>
<p style="text-indent: 0.74cm; margin-bottom: 0cm;"   >白色 接板子上的
<span lang="en-US"   >TX </span>（写）</p>
<p style="text-indent: 0.74cm; margin-bottom: 0cm;"   >绿色 接板子上的
<span lang="en-US"   >RX </span>（读）</p>
<p style="text-indent: 0.74cm; margin-bottom: 0cm;"   >红色
可以不接，如果接<span lang="en-US"   >VCC</span>，<span lang="en-US"   >OK</span>，你可以用不电源了（知道厂家为什么不提供电源了吧，哈哈），但不推荐，可能会造成<span lang="en-US"   >cubieborad</span>供电不足，一般的<span lang="en-US"   >usb</span>口只有<span lang="en-US"   >500ma</span>，<span lang="en-US"   >cubieboard</span>官方推荐是<span lang="en-US"   >2A</span>，但应个急还是很方便的。但也带不足，希望后面可以改进，就是不知道是开机还是关机，电源灯长红，哈哈哈。。。</p>
<p style="text-indent: 0.74cm; margin-bottom: 0cm;"   >连上<span lang="en-US"   >usb</span>转<span lang="en-US"   >ttl</span>线后。（<span lang="en-US"   >linux</span>对<span lang="en-US"   >USB</span>转<span lang="en-US"   >ttl</span>线，一般是带有驱动的，你可以不用装了（还是<span lang="en-US"   >linux</span>方便吧。））</p>
<p style="margin-left: 0.71cm; margin-bottom: 0cm;"   ><span lang="en-US"   >#
<font color="#000080"   >ls /dev/ttyUSB*</font></span></p>
<p style="margin-left: 0.71cm; margin-bottom: 0cm;"   ><span lang="en-US"   >/dev/ttyUSB0</span></p>
<p style="margin-left: 0.71cm; margin-bottom: 0cm;"   >
看一下是否有<span lang="en-US"   >USB0</span>或<span lang="en-US"   >1</span>之类的，如上例你可以用<span lang="en-US"   >screen
</span>命令连接。如果机器上没有。</p>
<p style="margin-left: 0.71cm; margin-bottom: 0cm;"   >
<span lang="en-US"   >#apt-get install screen</span></p>
<p style="margin-left: 0.71cm; margin-bottom: 0cm;"   >
安装一下就行了。</p>
<p style="margin-left: 0.71cm; margin-bottom: 0cm;"   >
<span lang="en-US"   >#screen /dev/ttyUSB0 11520 </span>
</p>
<p style="margin-left: 0.71cm; margin-bottom: 0cm;"   >
即可。但你现在可能什么都看不到。因为<span lang="en-US"   >cubieboard</span>开机是自动启动的。你的程序已经启动。按一下回车。或长按电源键<span lang="en-US"   >(10</span>秒<span lang="en-US"   >)</span>重启试试。</p>
<p align="LEFT"   style="text-indent: 0.74cm; margin-bottom: 0cm; line-height: 100%; page-break-inside: auto; widows: 0; orphans: 0; page-break-before: auto; page-break-after: auto;"   >
在一堆字符飞快的闪过你的屏幕以后，你将看到熟悉的<span lang="en-US"   >debian
</span>登录界面，恭喜你，费了这么大的劲成功了。</p>
<p align="LEFT"   style="text-indent: 0.74cm; margin-bottom: 0cm; line-height: 100%; page-break-inside: auto; widows: 0; orphans: 0; page-break-before: auto; page-break-after: auto;"   >
<span lang="en-US"   >INIT: Entering runlevel: 2</span></p>
<p align="LEFT"   style="text-indent: 0.74cm; margin-bottom: 0cm; line-height: 100%; page-break-inside: auto; widows: 0; orphans: 0; page-break-before: auto; page-break-after: auto;"   >
<span lang="en-US"   >[info] Using makefile-style concurrent boot in
runlevel 2.</span></p>
<p align="LEFT"   style="text-indent: 0.74cm; margin-bottom: 0cm; line-height: 100%; page-break-inside: auto; widows: 0; orphans: 0; page-break-before: auto; page-break-after: auto;"   >
<br>
</p>
<p align="LEFT"   style="text-indent: 0.74cm; margin-bottom: 0cm; line-height: 100%; page-break-inside: auto; widows: 0; orphans: 0; page-break-before: auto; page-break-after: auto;"   >
<span lang="en-US"   >Debian GNU/Linux 7.0 xxxxxxx ttyS0</span></p>
<p align="LEFT"   style="text-indent: 0.74cm; margin-bottom: 0cm; line-height: 100%; page-break-inside: auto; widows: 0; orphans: 0; page-break-before: auto; page-break-after: auto;"   >
<br>
</p>
<p align="LEFT"   style="text-indent: 0.74cm; margin-bottom: 0cm; line-height: 100%; page-break-inside: auto; widows: 0; orphans: 0; page-break-before: auto; page-break-after: auto;"   >
<span lang="en-US"   >xxxxxxx login: root</span></p>
<p align="LEFT"   style="text-indent: 0.74cm; margin-bottom: 0cm; line-height: 100%; page-break-inside: auto; widows: 0; orphans: 0; page-break-before: auto; page-break-after: auto;"   >
<span lang="en-US"   >Password: </span>
</p>
<p align="LEFT"   style="text-indent: 0.74cm; margin-bottom: 0cm; line-height: 100%; page-break-inside: auto; widows: 0; orphans: 0; page-break-before: auto; page-break-after: auto;"   >
<br>
</p>
<p align="LEFT"   style="text-indent: 0.74cm; margin-bottom: 0cm; line-height: 100%; page-break-inside: auto; widows: 0; orphans: 0; page-break-before: auto; page-break-after: auto;"   >
<br>
</p>
<p align="LEFT"   style="text-indent: 0.74cm; margin-bottom: 0cm; line-height: 100%; page-break-inside: auto; widows: 0; orphans: 0; page-break-before: auto; page-break-after: auto;"   >
<br>
</p>
<p align="LEFT"   style="text-indent: 0.74cm; margin-bottom: 0cm; line-height: 100%; page-break-inside: auto; widows: 0; orphans: 0; page-break-before: auto; page-break-after: auto;"   >
<br>
</p>
<p align="LEFT"   style="text-indent: 0.74cm; margin-bottom: 0cm; line-height: 100%; page-break-inside: auto; widows: 0; orphans: 0; page-break-before: auto; page-break-after: auto;"   >
叁考：</p>
<p align="LEFT"   style="text-indent: 0.74cm; margin-bottom: 0cm; line-height: 100%; page-break-inside: auto; widows: 0; orphans: 0; page-break-before: auto; page-break-after: auto;"   >
<span lang="en-US"   >http://linux-sunxi.org/Bootable_SD_card</span></p>
<p align="LEFT"   style="text-indent: 0.74cm; margin-bottom: 0cm; line-height: 100%; page-break-inside: auto; widows: 0; orphans: 0; page-break-before: auto; page-break-after: auto;"   >
<span lang="en-US"   >http://linux-sunxi.org/FirstSteps</span></p>
<p align="LEFT"   style="text-indent: 0.74cm; margin-bottom: 0cm; line-height: 100%; page-break-inside: auto; widows: 0; orphans: 0; page-break-before: auto; page-break-after: auto;"   >
<span lang="en-US"   ><font color="#0000ff"   ><a rel="nofollow" href="http://linux-sunxi.org/BuildingOnDebian"   >http://linux-sunxi.org/BuildingOnDebian</a></font></span></p>
