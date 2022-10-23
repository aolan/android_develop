# 安卓文件存储

* SharedPreferences： 以Map形式存放简单的配置参数；
* ContentProvider： 将应用的私有数据提供给其他应用使用；
* 文件存储：以IO流形式存放，可分为手机内部和手机外部（SD卡等）存储，可存放较大数据；
* SQLite：轻量级、跨平台数据库，将所有数据都存放在手机上的单一文件内，占用内存小。

## 一、SharePreferences

Android中提供三种方法获取SharedPreferences对象

### 1、context类中的 getSharedPreferences("文件名", "读写权限") 方法

* Context.MODE_PRIVATE：只能被本应用读写
* Context.MODE_WORLD_READABLE：能被其他应用读，不能写
* Context.MODE_WORLD_WRITEABLE：能被其他应用写，但建议使用，可能会导致应用不安全


### 2、Activity 类中的 getPreferences()方法

这个方法和 Context 中的 getSharedPreferences()方法很相似，不过它只接收一个操作模式参数，因为使用这个方法时会自动将当前活动的类名作为 SharedPreferences 的文件名。

### 3、PreferenceManager 类中的 getDefaultSharedPreferences()方法

这是一个静态方法，它接收一个 Context 参数，并自动使用当前应用程序的包名作为前缀来命名 SharedPreferences 文件。




## 二、内部存储

不用申请权限，卸载应用会跟着删除，root权限查看，app私有，外部应用是无法访问的，用户也无法操作。

* 获取应用程序内部存储的根目录

```kotlin
// 系统版本 >= 6.0，路径为 /data/user/0/${packagename}/
// 系统版本 < 6.0，路径为 /data/user/${packagename}/
context.dataDir
```

* 获取cache目录（主要用于存储应用使用过程中产生的缓存数据）

```kotlin
// 目录为：/data/user/0/${packagename}/cache
context.cacheDir
```

* 获取files目录（主要用于存储配置文件、敏感数据等）

```kotlin
// 目录为：/data/user/0/${packagename}/files
context.filesDir
```

* 获取apk路径

```kotlin

// 路径为：/data/app/~~CmbCAk6LSdOEKzMH2AIsbA==/${packagename}-6ttPe1AKrBu3sKUC6NJXxQ==/base.apk
val appInfo = context.packageManager.getApplicationInfo(packageName, 0)
appInfo.sourceDir
```

* Share Preferences 路径

```/data/user/0/${packagename}/shared_prefs/*.xml ```


* 获取 database 文件路径（/data/user/0/${packagename}/databases/*.db）

```kotlin
context.getDatabasePath("db名称")

```

* 获取lib目录

```kotlin

// 目录为：/data/app/~~CmbCAk6LSdOEKzMH2AIsbA==/${packagename}-6ttPe1AKrBu3sKUC6NJXxQ==/lib/arm64
val appInfo = context.packageManager.getApplicationInfo(packageName, 0)
appInfo.natvieLibraryDir
```

## 三、外部存储

需要申请文件权限，注意Andorid权限申请权限兼容问题，判断SD卡挂载情况。用户可以删除，其他应用申请权限之后可以访问。


```kotlin
// 根目录路径为：/storage/emulated/0/
if(Environment.getExternalStorageState().equals(Environment.MEDIA_MOUNTED)) {
  val sdcardPath = Environment.getExternalStorageDirectory()
}
```


参考：
* https://www.jianshu.com/p/321ad3e8bb19
* https://juejin.cn/post/6844903594244702221
* https://www.jianshu.com/p/a39bc4b3a1a6
