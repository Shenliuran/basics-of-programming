# 第一章 简介

## 英文缩写

>名词缩写|全拼|中文
>|:----|:--|:--|
>ISP|Internet Service Provider|因特网服务提供商
>TCP|Transmission Control Protocol|传输控制协议
>FTP|File Transfer Protocol|文件传输协议
>SMTP|Simple Mail Transfer Protocol|简单邮件传输协议
>UDP|User Datagram Protocol|用户数据报协议
>IP|Internet Protocol|网际协议
>OSI|Open System Interconnection|开放系统互联

## 名词解释

+ 协议：一个协议定义了在两个或多个通信实体之间交换的报文格式和次序，以及报文发送和/或接收一条报文或其他事件所采用的动作
+ 协议分层：各层的所有协议被成文协议栈
    1. 应用层：网络应用程序及它们的应用层协议保存的地方。位于应用层的信息分组成为报文。如：HTTP, SMTP, FTP
    2. 运输层：在应用程序端点之间传送应用层报文。如：TCP，UDP。TCP提供面向连接的服务，UDP向它的应用程序提供无线连接服务
    3. 网络层：网络层传输的是数据报（datagram）。如：IP，路由选择协议
    4. 链路层：如：以太网，WiFi和电缆接入网的DOCSIS协议。链路层分组成为帧（frame）
    5. 物理层：将每一帧中的一个一个bit从一个结点移动到下一个结点
