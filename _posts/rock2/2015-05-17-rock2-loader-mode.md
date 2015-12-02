---
layout: post
title: Rock2如何进入loder mode?
category: Rock2
tags: [rock2,loder]
keywords: loder,rock2
description: Rock2如何进入loder 模式?
---

当板子如法启动，等待从PC通过USB OTG接口的命令，此时板子处于Loder mode。square baseboard有三个键，恢复键、重启键和电源键（recovery key, reset key and the power key）。当进入loder mode时，我们需要使用恢复键和重启键。

![此处输入图片的描述][1]

为了进入loder mode，你应该：

1. 给板子上电，红色led指示板子开机
2. 连接USB OTG接口和PC（注意，你必须先连接OTG线，然后按下面的键）
3. 按住恢复键（靠近WiFi天线的那个）
4. 短按重启键（靠近DC的那个）
5. 放开恢复键

现在，开发板应该处于 loder 模式了。

Windows

Linux：

确保你有USB ID 2207:320a，此时rock2 square 处于loder模式了。

```
lsusb
...
Bus 001 Device 018: ID 2207:320a
...
```

For developers：

在u-boot命令行，你可以输入rockusb来进去loder模式。

你还可以看：

[Rock2/square_bb/hardware][2]
[rock/Loader_mode][3]

[1]: http://radxa.com/mw/images/1/1e/Loader_mode.jpg
[2]: http://radxa.com/Rock2/square_bb/hardware
[3]: http://radxa.com/Rock/Loader_mode

参考：

- http://radxa.com/Rock2/square_bb/loader_mode  

