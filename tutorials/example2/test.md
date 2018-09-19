

### 验证集成结果
   * 提供的 ```SpeechExecutor``` 模块 包含开机启动,如未能开机启动,请通过```adb shell am startservice com.rokid.voicerec/.SpeechExecutor``` 来启动Demo的service,然后通过Log查看是否有前端语音事件以及asr/nlp相关的log信息,如果有则证明集成OK.如果没有,请参考下边的集成注意事项或者联系我们.

### 集成注意事项

 * 目前Android全链路前端语音识别部分仅支持32位armeabi-v7a so文件输出,64位支持正在开发中,敬请期待.
 * 由于前端拾音模块需要读取Mic数据,因此各个客户/集成开发者需要在hal层实现mic设备的open以及read等接口,并以```"mic_array"```为```HAL_MODULE_INFO_SYM``` 的 id.具体接口可参考[mic_array集成说明](introduce_mic_array.md),代码实现可参考 [mic_array.c](../../extra/mic_array.c) & [mic_array.h](../../extra/mic_array.h) 的实现(请右键另存为 将文件下载保存).目前支持的 mic 阵列数据采集格式至少为```16K/16bit/单通道``` 的数据格式.

