---
title: x5内核下video标签的使用情况
date: 2017-09-29 15:05:56
tags: [x5,video]
#categories: "分类A"
#description: 文章摘要文章摘要文章摘要文章摘要
---

x5内核常见于安卓版的 `手机QQ浏览器` `手机QQ` `微信`。iPhone内没有X5内核。

## 在x5内核下video的表现（主要描述微信内）
下面这段代码
``` html 
<video src="video/advideo.mp4" controls></video>
```
在开始加载后，video将会被接管播放，导致视频处于页面最顶层，部分手机还会自动全屏播放。
腾讯所属的域名下video标签不接管。即所谓的域名白名单，目前尚无加入白名单的方法

关于自动全屏的问题可以添加`playsinline` `webkit-playsinline`以及x5私有的`x5-playsinline`避免全屏。
``` html 
<video src="video/advideo.mp4" controls playsinline webkit-playsinline x5-playsinline></video>
```
至于置顶这个问题，主要原因便是因为接管后播放器不属于html元素，可以理解为另一个与video标签相同尺寸的窗口悬浮与页面之上，顾无法调整层次。
不过x5提供了一种叫`H5同层播放器`的video播放模式，使内核不使用播放器接管播放。
请先阅读[H5同层播放器接入规范](//x5.tencent.com/tbs/guide/video.html)

通过添加`x5-video-player-type="h5"`启用该模式
但是该模式会进入一种全屏状态，并且把video标签的矩形区域截取到该状态中居中显示（为什么我这么说呢，因为该状态下video标签矩形区域内的其他节点元素也会被显示，甚至video标签在屏幕外也行）
在这种模式下，可以实现自制播放器UI，弹幕等等需要在video上叠加显示的效果。
比如[bilibli](//www.bilibili.com)便是使用了此方法实现了在X5内核下的弹幕。
![img](bilibili.png)
除了接管播放与同层播放，再没有其他播放模式，所以全屏与置顶根据项目需求选一个坑跳啦。


# 未完待续