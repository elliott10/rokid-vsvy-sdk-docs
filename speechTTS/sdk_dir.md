# SDK生成产物目录结构

## config

* speech_config.json ---- sdk需要的与厂商相关的key/secret等信息,需要网站上生成后以此命名

## doc

 - 说明文档目录,整理完成后放进去

## java-libraries  文件列表

* jdk1.7  若编译器javac版本为java 1.7.x版本
 * rokid_speech.jar
* jdk1.8  若编译器javac版本为java 1.8.x版本
  * rokid_speech.jar

**说明**
* rokid_speech.jar    ---- 语音识别以及合成服务(speech/tts) 输入输出的java api接口封装

## shared-libraries 文件列表

* arm64-v8a
  * libc++_shared.so
  * librkcodec.so
  * librokid_opus_jni.so
  * librokid_speech_jni.so
  * libspeech.so
  * libuWS.so
*  armeabi-v7a
   * libc++_shared.so
   * librkcodec.so
   * librokid_opus_jni.so
   * librokid_speech_jni.so
   * libspeech.so
   * libuWS.so



