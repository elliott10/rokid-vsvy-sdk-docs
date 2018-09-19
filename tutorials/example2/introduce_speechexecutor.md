## SpeechExecutor 模块说明
### 模块功能简介
 - 该模块为与前端数据交互的中间桥接模块,源码集成编译全链路```SDK```后,在网络OK并且```turenproc```正常启动后,启动该模块的```SpeechExecutor```的```service```,即可建立与前端的数据通讯,可接收前端的激活/ASR/NLP等事件.

### 模块文件树
```
├── Android.mk
├── AndroidManifest.xml
├── assets
│   ├── exec_config.json
│   └── speech_config.json
├── libs
│   └── VoiceRecognize.jar
├── res
│   ├── drawable-hdpi
│   │   └── ic_launcher.png
│   ├── drawable-mdpi
│   │   └── ic_launcher.png
│   ├── drawable-xhdpi
│   │   └── ic_launcher.png
│   ├── drawable-xxhdpi
│   │   └── ic_launcher.png
│   ├── values
│   │   ├── strings.xml
│   │   └── styles.xml
│   ├── values-v11
│   │   └── styles.xml
│   └── values-v14
│       └── styles.xml
└── src
    └── com
        └── rokid
            └── voicerec
                ├── ActionToComponent.java
                ├── AutoStartReceiver.java
                └── SpeechExecutor.java

14 directories, 16 files
```

### 模块主要功能点
- ```assets/exec_config.json``` 文件
 - 此文件在 ```SpeechExecutor.java``` 中通过```loadConfigs()```方法读取,然后通过``` parseConsumerConfig(String json)```方法将配置文件中的配置解析到 ``` list ```中,以便后续做事件的分发处理.
- ```assets/speech_config.json``` 文件
 - 此文件在 ```SpeechExecutor.java``` 中通过```loadConfigs()```方法读取,然后通过``` parseSpeechConfig(String json)```方法将配置文件中的配置解析出来,然后初始化```VoiceRecognize```. 此处解析非常重要,如下四处配置,客户需自行配置,如配置有误,会造成语音交互异常
```
	'key': '',    ----用户在Rokid开发者网站上申请设备类型时生成的key
	'device_type_id': '',----用户在Rokid开发者网站上申请设备类型时生成的Type ID
	'secret': '',----用户在Rokid开发者网站上申请设备类型时生成的Secret
	'device_id': ''   ----用户设备唯一码,可在SpeechExecutor的源码中parseSpeechConfig函数中根据客户的获取方法进行修改
```

- ```libs``` 文件夹下```VoiceRecognize.jar``` 为```SpeechExecutor```模块依赖的```jar```,可根据实际```java```版本选择```SDK```中对应的```java```版本```jar```包来替换处理,默认使用```java 1.7```的```jar```.
- ```src``` 为```SpeechExecutor```模块```Java```端实现部分,
 - ```ActionToComponent.java``` 为将```exec_config.json```配置的```action```解析成```android```对应```Component```的工具类
 - ``` AutoStartReceiver.java``` 监听开机广播,然后启动```SpeechExecutor```的```service```,在```android M```版本之后```data```下应用无此权限,```system```应用在运行一次后才有此权限.
 - ```SpeechExecutor.java``` 模块逻辑主要实现部分,主要有一下几点:
```
    loadConfigs(); ----从文件中读取key/secret等信息,做为参数初始化SDK,另外初始化语音激活事件/ASR/NLP的消费者,具体的消费者需要用户根据实际实现来动态配置exec_config.json
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
此初始化动作将前端需要的一些配置(在 ```speech_config.jso``` 配置)传递过去,并建立与前端的通讯.同时设置回调函数接口```VoiceRecognize.Callback```接收前端```Voice```事件以及```ASR/NLP```消息.在建立通讯成功后,即可通过 ```VoiceRecognize.Callback``` 相关的回调接口拿到响应的```Voice/ASR/NLP```事件.

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