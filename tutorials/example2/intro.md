## Android 全链路系统集成

### 概述
- Rokid 全链路系统集成是指选择 Rokid 全链路 SDK 下载后,通过 Android 源码方式集成SDK,集成 SDK 成功后,可以获取Rokid 前端语音激活/降噪以及 Rokid 语音识别服务和语音合成服务的相关能力.
 - 前端语音能力
  - 将麦克风阵列中的语音数据转换成对应的前端语音激活/休眠等事件. Rokid 提供的前端语音能力可为开发者提供语音自身音源降噪处理/回声消除/环境噪音降噪处理等
 - 语音识别服务
  - 语音识别可以通过开发者提供的原始语音数据/经过算法处理过的语音数据识别成对应的自然语言(ASR),以及对应的自然语言处理(NLP)信息
 - 语音合成服务(TTS)
  - Rokid语音合成服务可以根据开发者提供的文字合成高质量的音频。

### 硬件示例
- 可参考Rokid官方提供的开发套件,获取方式: 从[Rokid官网](https://developer.rokid.com/#/)获取 rokid all in one 全栈语音解决方案 开发套件
- 目前支持硬件指标为:
 - RAM 512M及以上
 - Mic阵列支持 线2麦/线4麦/圈4麦/圈6麦

### 软件框架
- 支持的Android OS
 - 目前SDK支持Android4.4及以上系统
- SDK下载
 - 请在 [FTP](ftp://ftp-customer.rokid-inc.com:9921/speech_sdk/v2/DNN/)上下载SDK
- SDK目录结构
 - [SDK目录结构](sdk_dir.md) 
- 软件设计框架图
 - 框架图如下 ![](../img/softworare_frame.png)

### 集成
- step1
 - [配置前端配置文件](introduce_config.md)
- step2
 - [Audio Input Hal 实现](introduce_mic_array.md)
- step3
 - [集成sdk](introduce_prebuilt.md)
- step4
 - [验证](test.md)