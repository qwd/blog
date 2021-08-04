---
title: 不再支持非SSL接口连接
tag: dev
image: /assets/upload/https.jpg
ref: nossl
---

![https](/assets/upload/https.jpg)

随着我们在2014年将所有API接口进行SSL加密（HTTPS）访问以来，99%以上的用户都已经完成了迁移，使用上了更加安全的加密连接。为了全面执行加密访问，我们将在2016年12月31日正式关闭非加密访问，因此请目前还在使用HTTP（端口80）方式获取数据的用户注意，需要大家尽快完成切换。
<!-- more -->

切换方式很简单，将原有`http`改为`https`即可。

在我们正式关闭非加密连接之前不会再有通知，请各位周知。