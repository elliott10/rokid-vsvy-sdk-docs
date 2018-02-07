### 准备编译环境
> 注：我们源码只支持mac及linux平台编译

* 安装openjdk

安装方法查看openjdk的官方说明。需要1.7以上版本。(为后继步骤的方便，最好装1.8以上的版本)

mac上无方便的安装openjdk方法，可使用oracle jdk [openjdk1.8](https://pan.baidu.com/s/1c2Vut9Y)的版本。

配置环境变量

```
export JAVA_HOME=下载解压路径/jdk1.8.0_111
export CLASSPATH=$JAVA_HOME/jre/lib/rt.jar:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar
export PATH=$JAVA_HOME/bin:$PATH
```

* 安装android sdk命令行环境

打开[android开发官方网站](https://developer.android.com/studio/index.html?hl=zh-cn)
拉到页面最下方“仅获取命令行工具”，找到对应你操作系统的工具包下载并解压。
![](img/pic4.jpg)


下面以\<android_sdk_dir\>指代刚刚下载的android sdk命令行工具目录。

> 如果sdkmanager运行出错，检查你的JAVA_HOME环境变量，看是否指向jdk1.8以上的版本。

```
cd <android_sdk_dir>/tools/bin
./sdkmanager "ndk-bundle"　　　　　　　　安装ndk命令行工具
./sdkmanager "build-tools;27.0.1"     安装build-tools 最新的27.0.1版本
./sdkmanager "platforms;android-23"   获取android6.0的android.jar
```


> sdkmanager运行完以后，openjdk1.8的环境不是必须的

> 如果在编译本源码时，使用的是openjdk1.8环境，那么安装的build-tools版本需要27以上，如果使用的是openjdk1.7环境，build-tools版本只需在23以上即可

> android.jar只需android6.0以上的版本，可自行选择

以上步骤执行成功后，<android_sdk_dir>下会出现platforms, build-tools, ndk-bundle子目录。
![](img/pic2.jpg)


配置环境变量

```
export PATH=$PATH:<android_sdk_dir>/ndk-bundle
export ANDROID_SDK_ROOT=<android_sdk_dir>
export ANDROID_BUILD_TOOL_VERSION=27.0.1     根据你安装的build-tools版本指定
```
