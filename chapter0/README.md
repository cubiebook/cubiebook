CUBIEBOOK - The missing cubieboard manual
=========================================


# 前言

## 一句话介绍cubieboard
* cubieboard是一款基于ARM Cortex A8的开发板
* cubieboard可以运行LinuX和Android
* cubieboard相对开放（包括内核源代码，原理图）， 黑客友好
* cubieboard以排针的形式暴露出了96++个GPIO，可以扩展IO，LCD, CSI摄像头，SD卡，SPI，I2C，串口等
* cubieboard板载
    * SATA （接泊硬盘）
    * HDMI （接泊显示器、电视机）
    * NAND 4GB （可存储操作系统、引导系统或保存数据）
	* DDR3 1GB （可保持系统为冯-诺兼容）
    * TF   （可存储操作系统、引导系统或保存数据）
    * USB Host * 2 (可插入USB设备)
    * USB OTG     （可以作为USB Doget或者通过LiveSuit刷写板载NAND）
    * AUDIO in/out （分别可以插入耳机或者话筒）
    * Ethernet    （可以插入网线看视频）
* cubieboard可以硬件解码2160p的视频 （not full function now）
* cubieboard的GPU为ARM Mali 400


## cubieboard的介绍


cubieboard第一次正式亮相是2012年8月31号，由[cnx-soft](http://www.cnx-software.com/2012/08/31/49-cubieboard-allwinner-a10-open-hardware-development-board/)，一个报道嵌入式方面新闻的网站发表了一篇文章，介绍了这个还没有发布的49美金的ARM板。为什么还没发布就报道了呢？因为cnx-soft的网站站长要去度假了，他的朋友Tom跟他说，cubieboard预计是8月底发布。所以他事先写好文章，把时间定在8月31号自动发布，然后去度假了。接着，一个星期后瘾科技[报道](http://www.engadget.com/2012/09/05/cubieboard-for-developers/)了cubieboard，接着全世界都知道了cubieboard。

cubieboard最初推出来是为了推广位于中国珠海的芯片公司-全志科技的ARM SOC以及相关的开源软件社区和生态环境，利用成熟和稳定的芯片及软件(全世界有超过千万的设备运行着这些软件)给开发者提供一个低价的开发平台和吸引更多的开发者关注来自中国的芯片，并且想把这些来自中国的好的芯片用在更多的用途上。全志科技的系列ARM SOC代号sunxi，作为见证了sunxi社区从无到有，并且参与了建设这个社区，我感到十分荣幸。因为来自中国的芯片也能吸引全世界的开发者。中国已经变成了一个很酷的国家，我们有深圳，有华强北，我们制造了全世界大部分的电子产品。我们在世界的影响力越来越大。

我在学校学习的时候，用的是ARM9的开发板，买的时候花了不少钱，而且在当时已经是出来好几年的ARM芯片，虽然学习不需要很新的东西，但是我还是渴望能够上手比较新一点的ARM设备。cubieboard不仅给在校的学生们提供了一个价格在接收范围内的相对现代一点的ARM开发学习硬件平台，并且提供了一个全球开发者和爱好者的社区。在中国的学生可以在这个平台上和全球的开发者社区学习和交流，可以向开源软件项目提交代码，参与技术讨论，锻炼和丰富自己的项目能力。

