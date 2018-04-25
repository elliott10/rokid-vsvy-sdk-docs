## Android 前端拾音算法集成
### [概述](introduce.md)
- Rokid 系统集成是指选择Rokid电视方案SDK下载后，通过在android app形式集成前端算法SDK，为合作伙伴者提供以下能力
- USB-micro语音输入，语音可以通过外接USB Mic获得音频数据
- 前端语音能力，将麦克风阵列中的语音数据转换成对应的前端语音激活/休眠等事件. Rokid提供的前端语音能力可为开发者提供语音 AEC 降噪处理/回声消除处理等

### 硬件
- 可参考Rokid官方提供的开发套件,获取方式: 从[Rokid官网](https://developer.rokid.com/#/)获取 rokid all in one 全栈语音解决方案 开发套件
- 目前支持硬件指标为:
 - RAM >= 512M, CPU?
 - Mic阵列支持 线2麦/线4麦/圈4麦/圈6麦

### 软件框架
- 支持的Android OS
 - 目前SDK支持Android4.4及以上系统
- SDK下载
 - 请在 [FTP](ftp://ftp-customer.rokid-inc.com:9921/speech_sdk/v2/DNN/)下载SDK
- SDK结构
 - [SDK目录结构](sdk_dir.md)
- 软件设计框架图 ![](../../img/frontend_integ_sw_arch.png)

### 集成步骤
- 下载sdk后，解压并按以下步骤配置android studio,
 - 把.so文件放入androidstudio中app\src\main\jniLibs\armeabi-v8a\下
	![](images/armv7.png)
 - jar架包放入app\libs\目录下
	![](images/jarlib.png)
 - 配置文件放入\app\src\main\assets\configturen
	![](images/configturen.png)
- 配置权限
	![](images/quanxian.png)
### 验证
- 点击运行DemoTuren APP， 插入USB Mic，对USB MIC 说唤醒词“若琪”
- adb shell 下 观察logcat 输出，能看到如下log输出
	![](images/ruoqi.png)


