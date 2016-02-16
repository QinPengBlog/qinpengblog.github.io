---
layout: post
title: 一加1刷机
date: 2016-02-15
categories: blog
tags: [Android]
description: 记录这次刷机的过程。

---

本次折腾时间160214 22:15-160215 15:00

这次刷机的缘起是手机提醒Resurrection Remix ROM更新到v5.6.3 0213了，我想到这周就要回实验室了，准备刷个新的后稳定用着。

##备份

用钛备份备份。由于Android Marshmallow 6.0系统限制对外置存储的访问，钛备份不能把备份目录设置在手机U盘了。这次直接把备份设置到本地存储里面。然而我的一加1是16G版的，安装好的程序+从Blisspop换过来的时候的备份+新的备份远远超过16G，中途失败了一次。把以前的备份转移到电脑里面，统计了一下，竟然有1.5G。接着继续备份完APP和系统数据。

##下载ROM

在备份的时候，同步在电脑上下载ROM。访问了[Resurrection Remix](http://www.resurrectionremix.com/)官网,依次跳转到[下载界面](https://basketbuild.com/devs/resurrectionremix/bacon)，结果竟然打不开，加到破解GFW的列表里还是打不开。

登陆[一加官方论坛](http://www.oneplusbbs.com/forum.php)在玩机板块的一加一ROM专区寻找该ROM。结果只找到了V5.6.3 0212的版本。同时我意识到可能这个版本出了问题，所以他们才在0213推出新的迭代版本。但是苦于找不到最新的版本，无奈只能下载它了。在浏览的过程中发现TWRP Recovery更新到3.0了，从论坛里下载了适用于一加1的版本，也搜索到了它的[官方网站](https://twrp.me/)。

在论坛里看到最新的CM13似乎基带又换成4.0了。我上次刷机的时候（160203）记得似乎是从4.0换成3.0了。本来计划用上次刷机用的CM13 Nightly作为底包，这次不得已又下栽了CM13 Nightly 0214作为底包。

##梳理刷机流程
在ROM官网虽然没有打开下载地址，但是在第一次跳转的下载地址上发现了一个官方的更新流程：

UPDATE INSTRUCTIONS

- Download the latest build of Resurrection Remix ROM
- Take a nandroid backup
- Flash ROM using ClockworkMod or TWRP recovery
- Flash Gapps
- Wipe cache
- Wipe dalvik cache
- Reboot
- Enjoy!

按照这个流程不需要清除Data分区，能保留装好的APP，所以打算按照这个来。

##下载Gapps
Google一系列的框架和软件包应该有更新所以去找了一番。但是Blisspop时代我下载BanksGapps的地址也打不开了。该ROM官方推荐的BanksGapps的下载地址里的包没有更新。Google搜索到了另外一个似乎是BanksGapps官方的[下载地址](http://download.dirtyunicorns.com/files/gapps/banks_gapps/)。这个地址的两个包虽然命名不同，但是大小一样，所以我就下载了BANKS_GAPPS_6.XX.zip（更新时间是0209，大小是306M，另一个名字里有Dynamic）。后来在官方的说明里发现这了个确实一样，之所以这样做是为了保持BANKS_GAPPS_6.XX.zip更新地址的一致。

##Flash
Recovery里仍然能够挂在U盘，所以将ROM和CM13的ROM，Gapps和Xposed框架，TWRP 3.0放进U盘。
1. 重启进入Recovery
2. 清除cache,dalvik cache。
3. 挂载U盘。
4. 刷入TWRP 3.0。
5. 重启进入Recovery。
6. 依次刷入CM13 Nightly 0214，Resurrection Remix V5.6.3 0212，BANKS_GAPPS_6.XX.zip，Xposed V80。
7. 清除cache,dalvik。
8. 重启进入系统
 
##Bug
重启顺利，进入系统前的优化程序阶段，结果卡在优化Contact Storage这一步。再次重启，结果卡在开机动画。

只能重新四清（cache, dalvik cache, data, system）刷机。这次顺利进入系统。用钛备份还原APP和系统数据。因为我使用Google Now，所以想先验证一下这个Gapp是否仍能被Xposed的LocationReportEnable模块欺骗。在Xposed中启动各模块后，清除Google各程序的资料和缓存，打开VPN，登陆Google，结果提示本地区不能使用Google Now。回到Xposed发现提醒我Xposed框架未激活，可是刚才还是激活状态。重启后



---










