### 预置SDK

  * 将解压后的目录放到系统源码中,比如```/vendor/rokid/sdk_v2/``` 目录下,然后在此文件夹下添加如下 [sdk_v2.mk](../extra/sdk_v2.mk) ,同时按照以下步骤使sdk能够被系统编译到
   * 在系统源码的```device/{platform}/{product}/*.mk``` 最后(此mk文件可以在编译时被编译到) 中添加如下
   ```
      $(call inherit-product,vendor/rokid/sdk_v2/sdk_v2.mk) 
   ```
   * 在 config 文件夹加下 添加```Android.mk```文件 ,并添加如下内容
   ```
    LOCAL_PATH := $(call my-dir)
    $(shell mkdir -p $(TARGET_OUT))
    $(shell cp -r $(LOCAL_PATH)/workdir_cn $(TARGET_OUT)/)
   ```
   * 在 executable 文件夹 添加 ```Android.mk```,并添加如下内容
   ```
    LOCAL_PATH := $(call my-dir)
    $(shell mkdir -p $(TARGET_OUT)/bin)
    $(shell cp $(LOCAL_PATH)/turenproc $(TARGET_OUT)/bin)
   ```
   * 在 shared-libraries 文件夹下添加 ```Android.mk```,并添加如下内容
   ```
    LOCAL_PATH := $(call my-dir)
    ifeq ($(TARGET_ARCH),arm64)
        $(shell mkdir -p $(TARGET_OUT)/lib64)
        $(shell cp -r $(LOCAL_PATH)/arm64-v8a/* $(TARGET_OUT)/lib64)
    else
        $(shell mkdir -p $(TARGET_OUT)/lib)
        $(shell cp -r $(LOCAL_PATH)/armeabi-v7a/* $(TARGET_OUT)/lib)
    endif
   ```
   * 将预置到```system/bin/turenproc``` 可执行进程加入到工程的```init.*.rc```中,使之能够以 root 权限在开机启动,示例如下:
   ```
     service turenproc /system/bin/turenproc <port> <deviceName>
     class main
     user root
     group root root
  ```
  其中 port 为启动 turenproc 进程启动时所依赖的运行端口号,比如: ```30000```, ```deviceName``` 为对应平台的```TARGET_DEVICE``` 值,``` workdir_cn ``` 文件夹中 ```dnn.{deviceName}.cfg```文件中的```deviceName```必须与之保持一致.比如 ```deviceName``` 为 ```pebble``` ,则需要如下方式启动
  ```
     service turenproc /system/bin/turenproc 30000 pebble
     class main
     user root
     group root root
  ```

### 预置注意事项
-  提供的```SpeechExecutor``` 模块为一个Demo程序,此Demo模块的具体说明请参考[SpeechExecutor模块说明](introduce_speechexecutor.md).
- 目前Android全链路前端语音识别部分仅支持32位```armeabi-v7a``` so文件输出,64位支持正在开发中,敬请期待.

### 接口调用说明
-  客户集成SDK时,对前端VoiceEvent/ASR/NLP等事件自行开发时,请参考[Android全链路接口调用说明](api_voicerecognize.md) 以及Demo源码进行开发.
