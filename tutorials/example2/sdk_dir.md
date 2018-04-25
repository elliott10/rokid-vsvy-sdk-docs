# SDK生成产物目录结构
## config
* workdir_cn  ----前端mic硬件配置以及激活模型文件目录,其中```dnn.xxx.cfg``` 文件为配置激活词信息以及,```device.xxx.cfg``` 文件为麦克风阵列相关配置文件.```workdir_cn```目录中的配置文件一旦生成,不允许私自修改内容及文件名.

## doc
 - 说明文档目录

## example
 - 源码示例程序1(android 源码编译集成前端 + speech 的示例程序 ,目录:SpeechExecutor)

## executable
* turenproc   ---- 前端拾音服务 链接mic数据读取以及语音识别服务(speech)模块的可执行进程
 
## java-libraries  文件列表
* jdk1.7  若编译器javac版本为java 1.7.x版本
  * VoiceRecognize.jar
  * rokid_speech.jar
* jdk1.8  若编译器javac版本为java 1.8.x版本
  * VoiceRecognize.jar
  * rokid_speech.jar

**说明**
* VoiceRecognize.jar    -----前端拾音服务(turen)输入输出 的java api接口封装
* rokid_speech.jar    ---- 语音识别以及合成服务(speech/tts) 输入输出的java api接口封装

### shared-libraries 文件列表
*  armeabi-v7a
   * libc++_shared.so
   * libr2mvdrbf.so
   * libr2ssp.so
   * libr2vt.so
   * librasr.so
   * librfe.so
   * librkcodec.so
   * librkvoicerec.so
   * librokid_opus_jni.so
   * librokid_speech_jni.so
   * libsourcelocation.so
   * libspeech.so
   * libtensorflow_inference.so
   * libtfam.so
   * libtfrtl.so
   * libturen.so
   * libturenrpc.so
   * libuWS.so
   * libztvad.so

**说明**
* common
  * libc++_shared.so
* 语音识别以及合成服务相关
  * librkcodec.so
  * librokid_opus_jni.so
  * librokid_speech_jni.so
  * libspeech.so
  * libuWS.so
* 前端拾音服务相关(目前还没有arm64-v8a 的so库)
  * libr2mvdrbf.so
  * libr2ssp.so
  * libr2vt.so
  * librasr.so
  * librfe.so
  * librkcodec.so
  * libsourcelocation.so
  * libtensorflow_inference.so
  * libtfam.so
  * libtfrtl.so
  * libturen.so
  * libturenrpc.so
  * libztvad.so


