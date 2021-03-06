---
layout: post
title: '2019-02-21-玩转Linux-02-使用花生壳内网穿透远程登录无公网IP的deepin Linux'
date: 2019-2-21
author: fslong
cover: 'https://raw.githubusercontent.com/wiki/fslong520/blog/img/杂/2019.02.21/使用花生壳内网穿透远程访问deepin%20Linux/深度截图_deepin-terminal_20190221134934.png'
tags: linux
---
  
&emsp;&emsp;*“不积跬步无以至千里，不积小流无以成江海”，这个系列是我在玩Linux的时候写的一些东西。*  
   

---
&emsp;&emsp;首先本文主要讲在没有公网IP的情况下，怎么使用花生壳的内网穿透功能通过ssh远程登录到你的电脑，至于有些如ssh的操作将不会仔细叙述，主要是为了解决没有公网ip的问题（自己有有公网ip服务器的小伙伴请绕道，下回我再讲那个frp技术）。这个有什么用呢？比如在外面操作家里的树莓派，还比如远程登录自己的电脑做些事等等。原理很简单就是使用花生壳新建了一个端口映射用于在外网使用ssh远程登录。  

### 一、下载安装花生壳客户端  
 

&emsp;&emsp;官网地址：[下载花生壳客户端]('https://hsk.oray.com/download/')   
![](https://raw.githubusercontent.com/wiki/fslong520/blog/img/杂/2019.02.21/使用花生壳内网穿透远程访问deepin%20Linux/深度截图_选择区域_20190221124132.png)

**注意根据自己的系统选择对应的安装包，并使用相应代安装，以笔者为例，使用的是deepin（基于debian stretch）：** `sudo dpki -i phddns_3.0_x86_64`  
安装完界面如下：![](https://raw.githubusercontent.com/wiki/fslong520/blog/img/杂/2019.02.21/使用花生壳内网穿透远程访问deepin%20Linux/深度截图_选择区域_20190221124356.png)  

**注意：这里的终端不要关，后续还要用到这个SN码**。       

### 二、注册花生壳账户并开启内网穿透  

&emsp;&emsp;**1、注册账户并登陆很简单，我就不在这细说了，注册完进入管理中心**    
![](https://raw.githubusercontent.com/wiki/fslong520/blog/img/杂/2019.02.21/使用花生壳内网穿透远程访问deepin%20Linux/深度截图_选择区域_20190221132344.png)     
进去之后如下图：  
![](https://raw.githubusercontent.com/wiki/fslong520/blog/img/杂/2019.02.21/使用花生壳内网穿透远程访问deepin%20Linux/深度截图_选择区域_20190221132827.png)    
向下拉点击1域名，再点击壳2域名（壳域名是免费的所以我们要用），新注册的账户一般自动生成一个壳域名，就像我圈起来的系统默认开通那个一样，比较奇怪的。第二个是我自注册的，也是免费的。每个帐号只可以注册一个免费的自定义的壳域名，当然你还可以花钱注册其他的，壳域名是不用备案的比较方便的那种。这里我们就实验用，所以就用第一个好了。  
&emsp;&emsp;**2、添加设备**  
如图，点击左侧的花生壳，再点击添加设备：  
![](https://raw.githubusercontent.com/wiki/fslong520/blog/img/杂/2019.02.21/使用花生壳内网穿透远程访问deepin%20Linux/深度截图_选择区域_20190221133308.png)  
输入我们刚刚在终端中看到的SN码，并点击确认：  
![](https://raw.githubusercontent.com/wiki/fslong520/blog/img/杂/2019.02.21/使用花生壳内网穿透远程访问deepin%20Linux/深度截图_选择区域_20190221133341.png)    
然后我们就可以看到刚刚添加的设备了：  
![](https://raw.githubusercontent.com/wiki/fslong520/blog/img/杂/2019.02.21/使用花生壳内网穿透远程访问deepin%20Linux/深度截图_选择区域_20190221133539.png)  
&emsp;&emsp;**3、添加端口映射**  
点击刚刚新添加的设备进入管理中心（就是Oray开头的那串字母加数字）：  
![](https://raw.githubusercontent.com/wiki/fslong520/blog/img/杂/2019.02.21/使用花生壳内网穿透远程访问deepin%20Linux/深度截图_选择区域_20190221133610.png)  
让微信扫一扫激活呢，那就扫吧，扫完可能还要绑定你注册的花生壳帐号，按提示操作即可，比较简单，然后点击进入平台：
![](https://raw.githubusercontent.com/wiki/fslong520/blog/img/杂/2019.02.21/使用花生壳内网穿透远程访问deepin%20Linux/深度截图_选择区域_20190221133655.png)  
在左侧点内网穿透，再点新增映射，然后填写所需内容。其中，应用名称自定义即可，选择域名选择刚刚那个壳域名，映射类型选应用类，外网端口就选择动态，静态是要钱的（动态的也不是一直在变，我中午建立的端口映射，晚上的时候还没变），内网主机就是你电脑的局域网地址，需要使用静态ip，自行查询怎么设置即可，内网端口就用ssh默认的22端口吧，当然你也可以自定义，注意一一对一即可，然后点击确定：  
![](https://raw.githubusercontent.com/wiki/fslong520/blog/img/杂/2019.02.21/使用花生壳内网穿透远程访问deepin%20Linux/深度截图_选择区域_20190221134055.png)  
这时我们就可以看到刚刚建立成功的端口映射了（贷款只有1M，流量只有一个月1G）：  
![](https://raw.githubusercontent.com/wiki/fslong520/blog/img/杂/2019.02.21/使用花生壳内网穿透远程访问deepin%20Linux/深度截图_选择区域_20190221134526.png)  
如果提示添加失败没有找到设备，那就是你电脑ssh配置的问题或者花生壳服务没有开启，重启花生壳服务的命令很简单是 `sudo phddns restart`，开启了如果还不行，请检查ssh服务开启情况，关于ssh服务配置教程很多，我就不在这里讲了。  
&emsp;&emsp;**4、远程连接**  
如果上述一切正常，那么使用ssh的远程连接命令即可连接，终端中输入`ssh [被连接电脑用户名]@[壳域名地址] -p [端口映射分配到的端口号]`  
![](https://raw.githubusercontent.com/wiki/fslong520/blog/img/杂/2019.02.21/使用花生壳内网穿透远程访问deepin%20Linux/深度截图_deepin-terminal_20190221134934.png)


&emsp;&emsp;**到这里教程就结束了，如果用其他的内网穿透服务商，其实也一样的，当然，用这个貌似很强大，但又好像啥都做不了，具体还需要你来开发！**


---   
  
> **声明：**
> 微信公众平台对于markdown支持不够友好，建议阅读原文。