# Mac安卓开发环境搭建

## 1. 安装JDK（这里我们采用JDK1.8）

下载链接：https://www.oracle.com/java/technologies/javase/javase-jdk8-downloads.html

采用默认的安装路径，jdk会被安装在`/Library/Java/JavaVirtualMachines/jdk1.8.0_301.jdk`目录下。

## 2. 多版本JDK管理


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



## 3. 安装android studio（下载最新版本即可）

### 3.1 下载

下载链接：https://developer.android.com/studio/

1. 不要直接点击页面顶部正中间的【Download Android Studio】，它会默认下载 `android-studio-2020.3.1.23-mac_arm.zip`，我试过，这个无法安装；
2. 滑动到页面底部，选择 `android-studio-2020.3.1.23-mac.dmg` 进行下载。

### 3.2 安装

1. 双击dmg打开，移动到application中；
2. 打开Android Studio，第一次打开会询问是否导入Android Studio 配置，因为我们是第一次安装，所以选择 Do not import settings；
3. 点击下一步，询问是否共享数据，我们选择 Don't send；
4. 然后会弹出错误 "Unable to access Android SDK add-on list"，原因是第一次启动，会在默认路径下检测是否有 Android SDK，如果没有就会报错，这里我们点击 cancel 先暂时跳过；
5. 然后进入配置向导，点击下一步，选择 Standard，然后点击下一步；
6. 选择完主题，然后点击 Finish，就会自动安装需要的组件。





