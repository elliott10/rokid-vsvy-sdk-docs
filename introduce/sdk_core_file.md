### SDK的核心组成
下表说明了Rokid SDK 2.0 中 每个组成部分的包名以及其对应的作用

| 安装包名称  | 包名  | 作用 |
|:------------- |:---------------:| -------------:|
| BearKid.far.apk| com.rokid.openvoice | 远场拾音服务并返回语音识别结果 |
| BearKid.near.apk| com.rokid.voicerec | 近场拾音服务并返回语音识别结果 |
| RKSpeechExecutor.apk| com.rokid.voicerec  | 负责语音识别结果分发及跳转|
| CloudEngine.apk | com.rokid.cloudengine   | 负责云端技能的应用栈运行管理器|
| CloudAppClient.apk | com.rokid.cloudappclient | 负责启动相应的云端程序|
| RKTtsService.apk| com.rokid.tts| TTS语音服务|