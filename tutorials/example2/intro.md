## Android 全链路系统集成

### [概述](introduce.md)

### 硬件示例
- 请从[Rokid官网](https://developer.rokid.com/#/)获取 rokid all in one 全栈语音解决方案 开发套件
- 目前支持硬件指标为:
 - RAM 512M及以上
 - Mic阵列支持 线2麦/线4麦/圈4麦/圈6麦

### 软件框架
- 支持的Android OS
 - 目前SDK支持Android4.4及以上系统
- SDK下载
 - 请在 [FTP](ftp://ftp-customer.rokid-inc.com:9921/speech_sdk/v2/DNN/)上下载SDK
- [SDK目录结构](sdk_dir.md)
- 软件设计框架图
![](../img/softworare_frame.png)

### 集成
1. [配置前端配置文件](introduce_config.md)
1. [Audio Input Hal 实现](introduce_mic_array.md)
2. [集成sdk](introduce_prebuilt.md)
3. [验证](test.md)