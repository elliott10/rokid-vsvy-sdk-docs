# SDK生成产物目录结构

##configturen
 - device.ttc.cfg   -----配置麦克风阵列
 - dnn.ttc.cfg   -----配置dnn
 - final.svd.mod   -----配置模型
 - phonetable   -----配置模型
 - word.meishile.cfg   -----激活词配置
 - word.ruoqi.cfg   -----激活词配置
 - final.ruoqi.mod ----激活词

## doc
 - 说明文档目录,整理完成后放进去

## example
 - 源码示例程序


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
   * libturenjava.so

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
  * libturenjava.so


