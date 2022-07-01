# Android studio 学习

## 版本

1. Android studio的版本刚开始让我误解了，截止2022-07-01，我下载的最新版本是 `Android Studio Chipmunk | 2021.2.1 Patch 1`，我以为是2021年发布的版本，其实不然，应该看第二行，即`built on May 19, 2022`。


```
Android Studio Chipmunk | 2021.2.1 Patch 1
Build #AI-212.5712.43.2112.8609683, built on May 19, 2022
Runtime version: 11.0.12+0-b1504.28-7817840 aarch64
VM: OpenJDK 64-Bit Server VM by JetBrains s.r.o.
macOS 12.4
GC: G1 Young Generation, G1 Old Generation
Memory: 2048M
Cores: 8
Registry: external.system.auto.import.disabled=true
Non-Bundled Plugins: org.jetbrains.kotlin (212-1.7.0-release-281-AS5457.46)
```

2. Android studio的版本规则有过一次调整，之前是版本规则是 `Android Studio v1.5.1（2015 年 12 月）`，但是在 `Android Studio v4.2.2` 之后，修改了版本规则，以便与IntelliJ IDEA（Android Studio 所基于的 IDE）保持一致。


参考：https://zhuanlan.zhihu.com/p/425663884


## 安装

1. Android Studio
2. Android SDK
3. Android Virtual Device	安卓模拟器
4. Perfomance（Intel HAXM）加速安卓模拟器的软件
5. Android SDK Toll

## 快捷键

| 描述       |    快捷键 | 
| :-------- | --------:|  
| 搜索 | shift两次 |  
| 查找类 |  cmd + o |  
| 查找文件 | cmd + shift + o | 
| 显示最近的文件 | cmd + shift + o | 
| 完成当前代码行 | cmd + shift + return | 
| 查看方法参数 | cmd + p |
| 查看方法 | fn + cmd + F12 | 
| 打开Project | cmd + 1 |
| 打开Favorites | cmd + 2 |
| 打开Terminal | fn + option + F12 |
| 隐藏所有窗口 | fn + shift + cmd + F12 |
| 运行 | ctrl + r |
| 调试 | ctrl + d |



## package 命名规则
采用反域名命名规则，全部使用小写字母。一级包名为com，二级包名lwz（为个人或公司名称，可以简写），三级包名guidecity（根据应用进行命名），四级包名ui或utils等（模块名或层级名），根据实际情况也是可以用五级包名，六级包名。

## 窗口描述

1. Android
2. Project
3. Problems   主要用于识别项目中某些文件编码错误或语法错误。


