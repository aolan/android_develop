# adb root 

命令用于重启 adbd 守护进程（Android Debug Bridge Daemon）以 root 权限运行。这意味着，当你执行 adb root 并且设备支持的话，adbd 将会以 root 用户身份重新启动，从而允许你通过 ADB 访问和操作设备上的所有文件和命令，而不仅仅是那些普通权限下的文件和命令。

# adb remount

是一个用于重新挂载 Android 设备的系统分区，使其具备可写权限的命令。通常情况下，Android 设备的系统分区是以只读（read-only）模式挂载的，以防止对系统文件的意外修改。然而，在开发和调试过程中，有时需要修改这些系统文件，这时就可以使用 adb remount 命令。在大多数情况下，执行 adb remount 需要设备已经通过 adb root 获取了 root 权限。如果设备不支持 adb root 或者你没有解锁 bootloader，则很可能无法成功执行 adb remount。

# adb install -d -r -t xx.apk    

允许降级安装
* -d 允许降级安装
* -r 保留数据重新安装
* -t 支持测试版 APK

# adb shell monkey -p packagename --ignore-crashes --ignore-timeouts --ignore-security-exceptions --pct-trackball 0 --pct-syskeys 0 --pct-nav 0 --pct-majornav 0 --pct-anyevent 0 -v -v -v --throttle 500 35000

跑 monkey 测试
* -p packagename 指定目标应用的包名
* --ignore-crashes 即使应用发生崩溃，测试也不会停止，monkey 会继续生成事件
* --ignore-timeouts 即使应用出现 ANR，测试也不会中断
* --ignore-security-exceptions 即使应用抛出权限相关异常，测试也会继续
* --pct-trackball 0   完全禁用轨迹球事件（Trackball Events）
* --pct-syskeys 0 完全禁用系统按键事件（如 Home 键、Back 键等）
* --pct-nav 0 完全禁用方向键导航事件（如 D-pad 按键）
* --pct-majornav 0 完全禁用主要导航事件（如菜单键、返回键等）
* --pct-anyevent 0 完全禁用其他未分类的随机事件
* -v -v -v -v 表示增加日志详细程度，最多可以指定三次（-v -v -v），表示输出最详细的日志信息
* --throttle 500 设置事件之间的延迟时间（单位为毫秒）
* 35000 monkey 将生成并发送 35,000 个随机事件

# adb shell am send-trim-memory packagename 80

这条命令的作用是通过 ADB 工具向指定的应用发送内存修剪（Trim Memory）信号，模拟系统通知应用释放内存的场景。它主要用于开发和测试环境中，帮助开发者了解应用在不同内存压力下的表现。

* am 是 Android 的 Activity Manager 工具，用于管理应用的活动（Activity）、服务（Service）以及其他组件
* send-trim-memory 这是 am 的一个子命令，用于向目标应用发送内存修剪信号，内存修剪信号通常由系统在内存不足时发出，通知应用释放不必要的资源
* 80 表示内存修剪的级别，具体对应于 ComponentCallbacks2.TRIM_MEMORY_COMPLETE。

# adb shell dumpsys meminfo packagename

这条命令用于查看指定应用的内存使用情况。它通过 dumpsys 工具获取 Android 系统中目标应用的详细内存信息，帮助开发者分析应用的内存占用、内存泄漏等问题。

* dumpsys 是 Android 的一个系统工具，用于查询和导出设备的各种运行时信息。它可以提供关于应用、服务、系统组件等的详细数据。
* meminfo 是 dumpsys 的一个子命令，专注于内存相关信息。通过 meminfo，可以查看指定应用或整个系统的内存使用情况。

# adb shell am dumpheap packagename /data/local/tmp/myleakcanaryheapdump.hprof

这条命令用于触发 Android 系统生成目标应用的堆内存快照（Heap Dump），并将其保存为 .hprof 文件。.hprof 文件是一种标准的 Java 堆内存快照格式，可以用来分析内存使用情况、查找内存泄漏等问题。

* am 是 Android 的 Activity Manager 工具，用于管理应用的活动（Activity）、服务（Service）以及其他组件。
* dumpheap 这是 am 的一个子命令，用于生成指定应用的堆内存快照。它会捕获当前应用的 Java 堆内存状态，并将其保存到指定路径。

# adb pull /data/local/tmp/myleakcanaryheapdump.hprof  ~/Desktop

将 hprof 文件导出到本地桌面。

# adb shell ps | grep monkey

查找 monkey 进程信息，第一个数字就是进程id

# adb shell kill -9 processId

* -9 指定发送的信号类型为 SIGKILL。SIGKILL 是一种强制终止信号，无法被进程捕获或忽略，确保目标进程会被立即终止。

# adb shell "ps | grep monkey | awk '{print \$2}' | xargs kill -9"

合并以上两条命令，可以实现直接关闭 monkey 进程



