# 编译 AOSP 源码

## 1. 安装 repo
```shell
curl https://storage.googleapis.com/git-repo-downloads/repo > /usr/local/bin/repo
chmod +x /usr/local/bin/repo
```

## 2. 初始化 repo
```shell
mkdir ~/aosp_main
cd ~/aosp_main
repo init -u https://android.googlesource.com/platform/manifest -b main
```

## 3. 同步代码
```shell
repo sync -c -j8
```


参考链接：https://source.android.com/docs/core/architecture/16kb-page-size/build-flash-pixel8-16kb?hl=zh-cn
