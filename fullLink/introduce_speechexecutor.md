## SpeechExecutor 模块说明
### 模块功能简介
 - 该模块为与前端数据交互的中间桥接模块,源码集成编译全链路SDK后,在网络OK并且turenproc正常启动后,启动该模块的SpeechExecutor的service,即可建立与前端的数据通讯,可接收前端的激活/ASR/NLP等事件.

### 模块主要功能点
- 在SpeechExecutor service 的onCreate中做初始化动作,如下示例代码
```
    loadConfigs(); ----从文件中读取key/secret等信息,做为参数初始化SDK,另外初始化语音激活事件/ASR/NLP的消费者,这部分目前未实现
```
```
    voiceRecognize = new VoiceRecognizeBuilder()
			.setHost(turenParam.host)
			.setPort(turenParam.port)
			.setBranch(turenParam.branch)
			.setKey(turenParam.key)
			.setSecret(turenParam.secret)
			.setDeviceTypeId(turenParam.deviceTypeId)
			.setDeviceId(turenParam.deviceId)
			.setCallback(this)
			.build();
```
此初始化动作作用在于将前端需要的一些配置传递过去,并建立与前端的通讯.同时设置回调函数接口(VoiceRecognize.Callback)接收前端Voice事件以及ASR/NLP消息.在建立通讯成功后,即可通过VoiceRecognize.Callback相关的回调接口拿到响应的Voice/ASR/NLP事件.

- VoiceRecognize.Callback
```
    void onVoiceEvent(int id,Event event, float sl, float energy); ----接收前端Voice事件,第一个参数Event为具体的event值,第二个参数(sl)为寻向角度,第三个参数(energy)为语音的能量值,此值程序暂时不需要关心,只做调试使用.
```
```
    void onIntermediateResult(int id,String asr, boolean isFinal); ----接收ASR,第一个参数为ASR的具体内容,第二个参数表示此ASR为中间识别结果 还是最终识别结果.false代表中间识别结果,比如语音输入"今天天气怎么样"时,ASR会阶段性的返回"今天"/"今天天气"/"今天天气怎么样"
```
```
    void onRecognizeResult(int id,String nlp, String action);  ----nlp的识别结果,第一个参数代表语音命中的具体NLP,如果为本地应用,需要解析此nlp来执行响应动作,如果为云端应用,则需要解析第二个参数(action)来执行对应的协议内容.
```
```
    void onException(int id,int errCode); ----语音数据交互过程中出现异常,参数为异常的errCode
```
以上几个函数定义可参考详细的接口文档介绍[Android全链路接口调用说明](api_voicerecognize.md).