# 圈子App

![](https://i.imgur.com/7peLkFi.jpg)

## DEMO

### APP DEMO视频
10分钟精品视频展示与讲解APP。链接：https://pan.baidu.com/s/1bpSFWMr 密码：q99a

### 软件工程化开发总报告

64页PDF详细讲解软件工程化开发全过程。链接：[圈子App - 总报告 PDF](https://github.com/KevinWang15/circle/blob/master/%E5%9C%88%E5%AD%90App%20-%20%E6%80%BB%E6%8A%A5%E5%91%8A.pdf)

### 开题报告PPT
简明阐述我们为什么做这个APP。链接：[开题报告](https://github.com/KevinWang15/circle/blob/master/%E5%BC%80%E9%A2%98%E6%8A%A5%E5%91%8A.pptx)

### 技术分享
技术选型与系统架构&为什么。链接：[技术分享](https://github.com/KevinWang15/circle/blob/master/%E6%8A%80%E6%9C%AF%E5%88%86%E4%BA%AB.pptx)

## 设计宗旨
* 人和人之间形成各种各样的圈子（E.g. 班级、寝室、实验室、社团、公司）

* 现在有很多社交圈子App，却鲜有提高效率的“工作圈子”
* 我设计的是一个工作圈子、效率圈子

* 为一个人的所有圈子提供统一的入口，一个平台处理所有待办事项


## 技术宗旨
* 一套核心（用户系统、圈子系统、消息系统、ACL）
* 无限可能的插件（服务器插件+客户端插件）
* HTML跨平台实现，可以于iOS、android、微信上运行
  ![App架构示意图](https://i.imgur.com/YHM9014.png)

这种可插拔的模块化、内核插件分离设计，很符合app的业务需要。

# Kernel层设计详述
## User
用户相关系统，包括用户注册、登入、鉴权、个人信息设置等模块。

## Group
群组系统，包括群组的建立、基本信息设定、用户加入群组、用户邀请别的用户加入群组、群组头像的生成、最近群组信息更新等。包括访问群组内其他成员与@mention他们的接口。

## Message & Notification
消息提醒系统，给每个用户一个统一的收件箱接收所有的群组消息。消息分为3种优先级，任何插件层的具体服务都可以调用消息系统给用户发消息，消息的出口也分站内界面、推送、短信/邮件（当前未实现）等多种。用户点击消息，app自动跳转到消息发源的服务。

## Access Control List
（本功能暂未在代码中实现，仅为设计）权限控制系统，允许服务对每个用户设定不同的权限级别，授权不同的角色做不同的操作。在真正的应用场景下，这种设置是很必要的，比如只有Product Manager可以在看板中把一个项目从阶段1推进到阶段2，普通的程序员不行。但这个期末Project时间有限，现在做的是所有人都有所有权限。

# Plugin层功能
为了印证设计以及让App看起来详实一些，我挑选了5个Plugin进行实现，接下来将简单对它们进行说明。
## Contact
通讯录，非常简单的一个功能，主要示范如何读取同组联系人的信息。
另外，添加了把群里用户保存到手机通讯录的功能。

## Forum
论坛，一个标准的论坛功能，带发帖、回帖、浏览等功能。
添加了在论坛中@mention同组别的用户的功能，被@mention的人会收到通知，帖子被回也会收到通知。

## Netdisk
网盘（文件共享）功能， 比较实用的功能，支持圈内用户间分享文件。
支持给文件上tag标签，支持实用tag标签进行过滤。
对于文档类型的文件（doc、pdf、xls等），手机端可以直接点击下载并查看。
但对于非文档类型的文件，手机阅览很不方便，日后如果有时间完善这个程序，我希望做一个屏幕穿越功能：电脑端打开某一个网站，显示一个二维码，在手机里扫描那个二维码，自动进行“屏幕穿越”，把网盘的上传、下载功能都穿越到网页上。
或者一种不那么酷的方式是，为这整套app做一个PC端。

## Kanban
这是综合性较强的一个功能，常见于软件工程中的项目管理。类似一个高级版的TODOLIST，但是任务却分多个阶段，每个阶段可以设置deadline、设置子任务，每个子任务可以分配给不同的人完成。系统有一些复杂性，圈子的力量在这个系统中最能够体现。（设想一个用户同时在多个开发组，他能在消息中看到一个统一的待办事项，点击消息又能到某个具体开发组里，看整个项目的流程。做任务时遇到困难，他还可以添加子任务并分配给队友，以获得帮助）
![看板概念](https://i.imgur.com/T3d5LV0.png)

## 相册
简单的图片上传和在线查看功能，支持同时上传多张图片，图片可来源于相册或直接使用相机拍摄。

## （未实现）活地图
类似于微信定位实时分享，可以看到别的成员的地理位置，可以设置导航到他们身边。

## （未实现）AA账本
适用于寝室等圈子，某成员交了一笔费/买了一件公用的商品/付了一笔餐费，现在这里记一笔，并选择参与的成员。到月末/认为方便的时间，自动计算出划款数量，统一结算。

# App截图
![](https://i.imgur.com/h2TQrpz.png)
![](https://i.imgur.com/f5bujme.png)
![](https://i.imgur.com/gDzvX8N.png)
# 未来打算
## ACL
如前所述，ACL是一个重要的功能，还未能完成，如果项目有机会后续发展成为产品，第一个应该完成的就是它。

## SDK和Developer Guide
插件式的设计允许开发者开发任何自己想要的功能。
应该分别提供Server和Client的SDK，来让开发者方便地访问Kernel中的四大模块所暴露的接口，并用它们开发自己的业务。
这个功能在打后期可以试着上线，甚至可以做个圈子应用市场，潜力无穷啊。

## 网页客户端
手机App在某些情况下可能不是特别好用，特别是当我们在做一个效率工具的时候。所以，我还考虑开发一个功能完全一样的网页版客户端，这样能最大利用PC的优势，更加高效地办公。

## 微信集成
因为本来就是用HTML5做的，所以放在微信上跑并不难。只是需要去申请服务号，才能调用微信的定位、扫码接口，才能把微信绑定（或者直接用微信注册）和对用户的信息推送做在微信上。

# 程序代码运行方式
代码运行方式比较繁琐，如果想看效果直接运行apk就好，我已经部署在公网服务器。
## Server部署
Server使用了Laravel框架（Laravel.com），需要composer包管理器（getcomposer.org）
1. 解压缩Server源代码包
2. 安装composer
3. cd进工程目录
4. 执行composer install安装依赖库
5. chmod storage和bootstrap目录，确保webserver有写权限
6. 复制.env.example文件到.env文件，并修改参数，配置DB_HOST、API_DOMAIN等信息
7. 建立数据库（需要和.env中信息对应）
8. 运行php artisan migrate和php artisan db:seed，来初始化数据库
9. 运行php artisan route:cache和php artisan api:cache
10. 安装Redis并开启Redis服务
11. 配置后台服务运行php artisan queue:work，配置计划任务每隔1分钟运行php artisan schedule:run
12. 应当可以正常运行，出现500可以看./storage/logs/laravel.log

## Client部署
Client端使用了Ionic框架（基于Angular 4）和Apache Cordova混合App框架
开发、编译和打包中大量使用NodeJS脚本，所以需要先下载NodeJS（推荐版本6.x）
假设已经安装好NodeJS、JDK和Android SDK，你需要按照如下步骤编译
1. 解压缩Client源代码包
2. cd进工程目录
3. 执行npm install安装依赖库
4. 执行npm install -g cordova
5. 执行npm install -g ionic
6. 执行ionic platform add android
7. 复制./src/config/environment.ts.example到./src/config/environment.ts并修改其内容，指向后端
8. 执行ionic run android或者ionic build android


# 联系方式
王轲  14307130048@fudan.edu.cn
![](https://i.imgur.com/q19lzLL.png)
