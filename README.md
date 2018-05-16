---
title: iOS接口生成器
author: 邵存将
date: 2017-7-31 10:30:50
categories:
- 工具化
tags: 
- RAP 接口生成器
---


## 项目背景
当前开发项目每个版本都有一堆接口，这些接口开发编写对应的model,dao和业务调用层代码需要耗用大量时间，而且都是重复无意义的工作，基于此开发了个接口生成器

使用接口生成器的好处：

-  只需要修改一个项目ID就可以自动生成所有的接口，数据模型，接口调用层，大量节省接口部分的开发时间
-  可以在服务端未提供数据的情况下，自动MOCK数据做开发调试，会自动根据接口文档生成Mock接口,这些接口会自动生成模拟数据,支持复杂的生成逻辑
-  可以通过项目ID自动生成IOS端,ANDROID端的接口SDK和java后端的接口模板 目前仅做了IOS端的支持
-  规范接口的详细设计文档

## 解决方案 

-  利用RAP制作接口的详细设计
-  通过接口生成器将RAP的接口设计文档转化为接口SDK

## 如何使用接口生成器
-  利用RAP生成接口设计文档 
   
   RAP的使用教程请查看下面的地址:

   https://github.com/thx/RAP/wiki/home_cn 

   以下是作业系统达标作业版本通过RAP生成的设计文档 如图1所示 

   项目接口文档地址:

   http://rapapi.org/workspace/myWorkspace.do?projectId=21739#213623

   用户名 a7573770 密码 7888067

   ![](images/1.png)
   其中项目ID就是图1中的21739 

   图1中接口描述用于表示生成model的类名

-  从GITHUB下载接口生成器

   下载地址如下

   https://github.com/7573770/InterfaceGenerator.git

   下载完点击运行工程生成下面窗口 修改项目ID为RAP设计文档的ID 

   如达标作业版本的项目ID为上图标注的21739,项目前缀为自己工程的项目前缀 

   运行项目显示图2的界面：

   ![](images/2.png)

   点击生成文件选择生成文件的目录 即可在该目录下生成对应的接口SDK 打开刚才选择的目录 直接把生成的文件拷贝到自己项目中就可以使用了  
   比如达标作业生成的文件结构 如图3所示 其中service为接口调用层 每个模块生成一个service  

  ![](images/3.png)

  接口调用示例：

    RAPStandardOperationService *service=[[RAPStandardOperationService alloc]init];

    [service getsubject:@"nb300" success:^(NSArray<RAPSubject *> * list) {

    } failure:^(NSError *error) {
 
    }];

   接口生成完默认采用的是MOCK数据 要改成自己服务端数据只需要打开生成的RAPConfig文件
   将RAPISMOCK改为NO  RAPBASEURL改为自己的服务器地址就可以了 其中RAP为项目前缀 
   如下图4所示:
   
![](images/4.png)
