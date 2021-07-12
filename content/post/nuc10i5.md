---
title: "NUC10i5 Hackintosh Catalina10.15.5"
date: 2020-07-17T12:53:37+09:00
tags: ['NUC', 'Hackintosh','Catalina']
---
###  Hackintosh Catalina10.15.5

文章内容适用于NUC10i5 and NUC10i7机型（已修改)

intel nuc10i5 model and nuc10i7 model

<!--more-->
如果想安装Catalina10.15.6和OpenCore0.6.0的话   [请点击这里](www.baidu.com) <br>
对于黑苹果的集成无线网络问题，还没有找到驱动的方法。<br>
如果有条件可以选择USB网卡。<br>
除此之外，隔空投送，iPad随航需要调整驱动。<br>
本教程使用OpenCore0.5.9 以及MacOS Catalina10.15.5作为镜像安装。<br>
本教程暂时使用MacOs作为启动盘制作教程 <br>

1. 需要准备一个U盘，容量最好16G以上.
2. 下载[OpenCore0.5.9](https://github.com/acidanthera/OpenCorePkg/releases) 选择OpenCore-0.5.9-DEBUG.zip 或者 OpenCore-0.5.9-RELEASE.zip Debug版本的报错信息更为详细，如果没有需要这类信息可以使用RELEASE.
3. 下载[GibMacOS](https://github.com/corpnewt/gibMacOS) ---下载苹果系统镜像.
4. 下载[NUC10所需要的EFI文件](https://github.com/SummerSnowWinterCat/NUC10EFI) ---启动盘所需要的EFI文件.
5. 下载[MountEFI](https://github.com/corpnewt/MountEFI)----打开隐藏的EFI盘.
6. 下载[ProperTree](https://github.com/corpnewt/ProperTree) ----修改plist文件.
7. 下载[GenSMBIOS](https://github.com/corpnewt/GenSMBIOS) ----生成MAC型号以及序列号.
8. 额外的蓝牙驱动 需要自己下载适用的蓝牙kext

### 安装步骤
1. 打开GibMacOS里的gitMacOS.command 选择macOS的版本，如果是catalina10.15.5就是选择 1 然后回车，自动开始下载。。。。
2. 下载完成后，运行BuildmacOSInstallApp.command 然后添加刚刚下载MACOS镜像的路径到这里。从gitMacOS里面找到Catalina或者是别的镜像，把文件夹拖至此处，按回车。
 >然后就可以发现镜像文件夹里面出现了一个Install macOS xxx的文件。
 3. 使用Mac自带的DiskUtility软件格式化U盘
 4. 格式化完成后，打开命令行输入
 
 ```sudo macos的路径/Contents/Resources/createinstallmedia --volume /Volumes/USBMemory的名称```
 
 >macos路径选择刚刚下载好的MacOS文件夹内的Install macOS .app文件 Volumes后面改成自己U盘的命名
 
 ```例子：sudo /Applications/Install\ macOS\ Catalina.app/Contents/Resources/createinstallmedia --volume /Volumes/MyVolume```
 >这一行不要复制，作为参考！<br>
 
 回车后输入Y进行镜像导入 等待完成。。。需要蛮久的时间，具体时间得看U盘的速度
 
5. 使用MountEFI打开隐藏分区EFI

选择安装好后的U盘盘符 并输入数字，即可打开隐藏分区。

6. 打开访达找到EFI盘，将NUC10EFI文件夹整个移动到里面即可

7. 接下来修改BIOS，启动NUC10进入BIOS界面

>Advanced > SATA Controller(s)  = Enabled

>Advanced > SATA Mode Selection  = AHCI

>Onboard Devices >  HD Audio = Enabled

>Onboard Devices >   Thunderbolt(TM) Support = Enabled

>Onboard Devices >  WLAN = OFF

>Security >  SGX Owner EPCCHs = Factor Default

>Secure Boot > Secure Boot  = Disabled

>Boot > Boot Option #1 = OpenCore

Boot的地方选择要启动的U盘为第一个Option

去除FastBoot

>Boot > Fast Boot  = OFF

8. 按下F10保存并退出，启动U盘的引导

9. 没出问题的话，即可开始安装MACOS

10. 安装完以后，使用MountEFI打开安装好后的盘符里的EFI，打开EFI盘符，将U盘里的EFI文件夹拖至系统的EFI里。

11. 打开GenSMBIOS ，运行GenSMBIOS.command

>先选择 1 安装MacSerial 然后选择 2 把系统EFI里 OC文件夹内的Config.plist拖入命令行

>选择3 生成虚假机器型号 比如 MacMini8，1 或者iMac 9，1 等 然后选择4生产UUID 最后输入5 后 退出关闭命令行

>!推荐i5机型使用MacMini8，1 i7机型使用iMac 或者MacMini8，1

12. 重启系统 （如果无法启动，BIOS里选择安装好后的盘符）

13. ProperTree 是用来无损修改plist的程序，如果需要消除启动时候会显示的命令代码，可以用ProperTree来修改plist。

> NVRAM > boot -args : -v <--remove

记得按command+s进行保存后，重启系统

【如有什么问题 可以在[下面提问](https://github.com/SummerSnowWinterCat/NUC10EFI/issues)！】

![](/nuc10i5/4.jpg)
