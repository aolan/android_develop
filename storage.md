# 安卓文件存储

* SharedPreferences： 以Map形式存放简单的配置参数；
* ContentProvider： 将应用的私有数据提供给其他应用使用；
* 文件存储：以IO流形式存放，可分为手机内部和手机外部（SD卡等）存储，可存放较大数据；
* SQLite：轻量级、跨平台数据库，将所有数据都存放在手机上的单一文件内，占用内存小。

## 知识储备

### 内部存储

不用申请权限，卸载应用会跟着删除；用户无法查看该目录，除非进行root。该路径是APP私有路径，其他应用无法访问。

### 外部存储

需要申请文件权限，注意Andorid权限申请权限兼容问题，判断SD卡挂载情况。用户可以删除，其他应用申请权限之后可以访问。


### 外部存储


## 路径介绍

### 1. 内部存储根目录

目录：```/data```

获取方法：```Environment.getDataDirectory()```

### 2. 应用安装目录

目录：```/data/app/```

获取方法：

```kotlin
val appInfo = context.packageManager.getApplicationInfo(packageName, 0)
val path = appInfo.sourceDir
```

### 3. 获取lib目录

目录：```/data/app/xxx/$packageName-xxx/lib/arm64```

获取方法：

```kotlin
val app = context.packageManager.getApplicationInfo(packageName, 0)
app.nativeLibraryDir
```

### 4.  应用数据根目录

目录：```/data/user/0/$packageName/```

获取方法：	```Context.dataDir```

### 5.  应用数据缓存目录

用途：主要用于存储应用使用过程中产生的缓存数据。

目录：```/data/user/0/$packageName/cache/```

获取方法：```context.cacheDir```

### 6. 应用数据库目录

目录：```/data/user/0/$packageName/databases/```

获取方法：```context.getDatabasePath('user.db')```

### 7. 应用文件存放目录

用途：主要用于存储配置文件、敏感数据等。

目录：```/data/user/0/$packageName/files/```

获取方法：```context.fileDir```

### 8. SharedPreferences目录

目录：```/data/user/0/$packageName/shared_prefs/```

获取方法：一般不会直接编辑里面的文件，存放的是一些数据量较小的键值对。

读方法：

```kotlin
val sharedPreferences = context.getSharedPreferences("文件名", Context.MODE_PRIVATE)
val value = sharedPreferences.getBoolean("key", false)
```

写方法：

```kotlin
val sharedPreferences = context.getSharedPreferences("文件名", Context.MODE_PRIVATE)
sharedPreferences.putBoolean("key", false).apply()
```

其中权限包括：

* Context.MODE_PRIVATE：只能被本应用读写
* Context.MODE_WORLD_READABLE：能被其他应用读，不能写
* Context.MODE_WORLD_WRITEABLE：能被其他应用写，但建议使用，可能会导致应用不安全

### 9. 外部存储根目录

目录：```/storage/emulated/0/```

获取方法：

```kotlin
// 先判断是否挂载了SD卡
if(Environment.getExternalStorageState().equals(Environment.MEDIA_MOUNTED)) {
  val path = Environment.getExternalStorageDirectory()
}
```


参考：
* https://www.jianshu.com/p/321ad3e8bb19
* https://juejin.cn/post/6844903594244702221
* https://www.jianshu.com/p/a39bc4b3a1a6
