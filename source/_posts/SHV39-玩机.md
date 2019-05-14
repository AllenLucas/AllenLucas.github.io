---
title: SHV39 玩机
copyright: true
date: 2019-05-14 15:00:15
tags:
---

[TOC]

## 无root，去除叉号，感叹号

1. 删除变量：（删除以后默认启用） `adb shell settings delete global captive_portal_mode`
2. 关闭检测：  `adb shell settings put global captive_portal_mode 0`
3. 查看当前状态：`adb shell settings get global captive_portal_mode`
4. 删除（删除默认用HTTPS）: `adb shell settings delete global captive_portal_https_url` `adb shell settings delete global captive_portal_http_url`
5. 分别修改两个地址 : `adb shell settings put global captive_portal_http_url http://captive.v2ex.co/generate_204` `adb shell settings put global captive_portal_https_url https://captive.v2ex.co/generate_204`

操作完毕，飞行模式切换下就可以了
![此处输入图片的描述][1]

## 日系手机升级

1. 良好的wifi网络
2. 良好的日本节点
3. SSR点击选项设置，勾选允许来自局域网的连接，去掉服务器负载均衡
   ![此处输入图片的描述][2]
4. 然后电脑运行cmd 命令行ipconfig查询ip地址
5. 手机连接同样的WiFi，手动修改，输入电脑的ip，及端口
   ![此处输入图片的描述][3]
6. SSR全部设置为全局（系统代理模式 or 代理规则）
7. 等待wifi的叉号消失，去进行升级(OTA)
8. 若无法更新，尝试恢复出厂设置

[1]: https://attach.bbs.miui.com/forum/201804/03/213805z55c55is5x3g5s5x.png.thumb.jpg
[2]: http://imgsrc.baidu.com/forum/w=580/sign=e105d952434a20a4311e3ccfa0529847/766d57166d224f4a82b7f25305f790529922d1df.jpg
[3]: http://imgsrc.baidu.com/forum/w=580/sign=97fa14df22dda3cc0be4b82831e83905/b29f5f36acaf2edd7f00c4a9811001e938019310.jpg