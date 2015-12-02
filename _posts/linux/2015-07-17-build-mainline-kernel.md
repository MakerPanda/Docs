---
layout: page
title: 为Rock编译3.18及以上Linux内核
category: Linux
tags: [linux,内核]
keywords: 产品, 配置
description: 
---

# 为Rock编译3.18及以上Linux内核  

## 1.环境需要  

* Ubuntu系统  
* GCC4.9+（4.8不支持）  

## 2.获取源码  

* kernel v3.18:
https://www.kernel.org/pub/linux/kernel/v3.x/linux-3.18.11.tar.xz  
  同时还要获取配置文件  
  `wget http://rockchip.fr/radxa/linux/rockchip_defconfig -O arch/arm/configs/rockchip_defconfig`  
  `wget http://rockchip.fr/radxa/linux/rk3188-radxarock.dts -O arch/arm/boot/dts/rk3188-radxarock.dts`  

* Kernel v4.0:`git clone -b stable --depth 1 git://git.kernel.org/pub/scm/linux/kernel/git/next/linux-next.git`  
  获取配置文件  
  `wget http://rockchip.fr/radxa/linux/rockchip_defconfig -O`  
  `wget http://rockchip.fr/radxa/linux/rk3188-radxarock.dts -O arch/arm/boot/dts/rk3188-radxarock.dts`  

## 3.编译内核  

`export ARCH=arm`  
`export CROSS_COMPILE=arm-linux-gnueabihf-`  

上面的CROSS_COMPILE变量是指gcc编译器的路径名，可能需要根据具体情况修改  

## 4.创建boot镜像  

* 如果你没有mkbootimg工具的话，按照下面的方式下载，如果有的话，则跳过  
	`git clone https://github.com/neo-technologies/rockchip-mkbootimg.git`  
	`cd rockchip-mkbootimg`  
	`make`  
	`sudo make install`   
	`cd ..`  

* 对于V3.18之后的内核，我们还需要把设备树（dtb）附加到内核镜像中，因为现在U-boot还不支持这个操作  
	`cat arch/arm/boot/zImage arch/arm/boot/dts/rk3188-radxarock.dtb > zImage-dtb`  

* 制作虚拟磁盘  
	`git clone https://github.com/radxa/initrd.git`  
	`find . ! -path "./.git*"  | cpio -H newc  -ov > initrd.img`  

* 开始打包生成  
	`mkbootimg --kernel zImage-dtb --ramdisk initrd.img -o boot.img`  

得到镜像booting.img!  

然后再利用烧录工具进行烧录就可以了 ！  

