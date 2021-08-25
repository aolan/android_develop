# Mac安卓开发环境搭建

## 1. 安装android studio（下载最新版本即可）

访问链接：https://developer.android.com/studio/

## 2. 安装JDK（这里我们采用JDK1.8）

下载链接：https://www.oracle.com/java/technologies/javase/javase-jdk8-downloads.html

采用默认的安装路径，jdk会被安装在`/Library/Java/JavaVirtualMachines/jdk1.8.0_301.jdk`目录下。

## 3. 多版本JDK管理


如果电脑上安装了较多版本的JDK，可以采用jenv工具来进行管理：https://github.com/jenv/jenv

```shell

# 安装jenv工具
brew install jenv

# 允许jenv引入export插件，来管理JAVA_HOME
jenv enable-plugin export

# 检查jenv是否安装完毕
jenv doctor

```

执行 `jenv doctor`之后，输出下面的日志，说明jenv安装成功：

```
[OK]	JAVA_HOME variable probably set by jenv PROMPT
[OK]	Java binaries in path are jenv shims
[OK]	Jenv is correctly loaded
```

执行 `jenv add /Library/Java/JavaVirtualMachines/jdk1.8.0_301.jdk/Contents/Home`，该版本的JDK将会被添加到jenv中，如何验证呢？

执行 `jenv versions`，就能看到刚刚安装的JDK版本，例子中的版本为 `1.8.0.301`

切换JDK版本，执行 `jenv local 1.8.0.301` 命令即可，重启命令行工具，即可让所有的shell生效。

