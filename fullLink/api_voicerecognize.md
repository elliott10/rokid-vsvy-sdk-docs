###VoiceRecognize接口说明

rkvoicerec.jar中包含`VoiceRecognize`和`VoiceRecognizeBuilder`两个比较重要的类。使用`VoiceRecognizeBuilder`设置Rokid账号信息就能得到一个`VoiceRecognize`对象，账号获取方式见**附件1**。下面详细介绍`VoiceRecognize`内部类和接口定义：

#### 1. 内部类:
|类型|名称|描述|
|:--:|:--|:--|
|enum|Action|语音控制意图枚举定义：</br>`ACTION_SET_STATE_AWAKE` 设置当前从休眠状态进入激活状态，此时不用说激活词直接语音命令即可，也可以通过说休眠词进入休眠状态</br>`ACTION_SET_STATE_SLEEP` 设置当前从激活状态进入休眠状态，此时可以通过唤醒词再次进入激活状态</br>`ACTION_OPEN_MIC` 打开麦克风，此时可以通过唤醒词进入激活状态</br>`ACTION_CLOSE_MIC` 关闭麦克风，需要打开麦克风才能通过唤醒词唤醒|
|enum|Event|语音唤醒事件枚举定义：</br>`EVENT_VOICE_COMING` 激活即将开始</br>`EVENT_VOICE_LOCAL_WAKE` 本地已经激活</br>`EVENT_VOICE_START` 开始上传VAD</br>`EVENT_VOICE_NONE` 二次确认结果为空，只出于已经在激活状态下，直接说语音命令</br>`EVENT_VOICE_ACCEPT` 云端二次确认通过</br>`EVENT_VOICE_REJECT` 云端二次确认不通过</br>`EVENT_VOICE_CANCEL` 取消当前上传VAD<br>`EVENT_VOICE_LOCAL_SLEEP` 通过休眠词从激活状态进入休眠状态|
|enum|ExceptionCode|异常状态定义：</br>`EXCEPTION_SERVICE_INTERNAL` 语音内部错误 </br> `EXCEPTION_ASR_TIMEOUT` ASR识别超时
|class|VtWord|激活词信息：`type` 激活词类型，`word`激活词中文字符表示形式，`pinyin`激活词拼音字符+音调表示形式(例：若琪 ruo4qi2，ruo为四声，qi为二声)|
|enum|Type|激活词类型枚举定义：`AWAKE`唤醒词，`SLEEP`休眠词，`HOTWORD`热词，`OTHER`保留|
|interface|Callback|接收识别结果的回调接口定义，详细介绍见第3节Callback接口说明|

#### 2. 公有函数：
|	|类型|名称|描述|
|:--|:--|:--|:--|
|接口||control|控制语音激活|
|参数|Action|action|控制意图|
|返回值||int|成功返回0；失败返回-1
    
|	|类型|名称|描述|
|:--|:--|:--|:--|
|接口||addVtWord|添加激活词|
| 参数|VtWord|vtWord|激活词信息|
|返回值||int|成功返回0；失败返回-1
    
|	|类型|名称|描述|
|:--|:--|:--|:--|
|接口||remoteVtWord|删除激活词|
|参数|String|content|需要删除的激活词utf-8字符串|
|返回值||int|成功返回0；失败返回-1

|	|类型|名称|描述|
|:--|:--|:--|:--|
|接口||getVtWords||
|参数|无|无|
|返回值||ArrayList|成功返回激活词集合；失败返回一个空的集合
    
|	|类型|名称|描述|
|:--|:--|:--|:--|
|接口||setSkillOption|同步客户端信息到云端|
|参数|String|skillOption|当前skill运行状态信息|
|返回值||int|成功返回0；失败返回-1

|	|类型|名称|描述|
|:--|:--|:--|:--|
|接口||updateStack|更新云端NLP栈信息|
|参数|String|currAppId|执行当前语音命令的应用AppId|
|参数|String|prevAppId|执行上一条语音命令的应用AppId|
|返回值||int|成功返回0；失败返回-1

#### 3. Callback接口说明：

|	|类型|名称|描述|
|:--|:--|:--|:--|
|接口||onVoiceEvent|语音事件回调接口|
|参数|Event|event|语音事件|
|参数|float|sl|当前唤醒角度(0到360度之间)|
|参数|float|energy|当前说话能量值(0到1之间的浮点数)|
|返回值|无||

|	|类型|名称|描述|
|:--|:--|:--|:--|
|接口||onIntermediateResult|语音识别中间结果，可能回调多次|
|参数|String|asr|语音转文字结果|
|参数|boolean|isFinal|是否是最终完整的语音转文字结果|
|返回值|无||

|	|类型|名称|描述|
|:--|:--|:--|:--|
|接口||onRecognizeResult|最终语音识别回调接口|
|参数|String|nlp|自然语义解析结果|
|参数|String|action|云端skill结果|
|返回值|无||

|	|类型|名称|描述|
|:--|:--|:--|:--|
|接口||onException|语音识别出错|
|参数|ExceptionCode|code|错误码|
|返回值|无||
   
#### 示例：

    import android.util.Log;
    
    import com.rokid.voicerec.VoiceRecognize;
    import com.rokid.voicerec.VoiceRecognizeBuilder;
    
    public class MainService extends android.app.Service implements VoiceRecognize.Callback{
    
        private String TAG = getClass().getSimpleName();
        private VoiceRecognize mVoiceRecognize = null;
    
        @Override
        public void onCreate(){
            VoiceRecognizeBuilder builder = new VoiceRecognizeBuilder();
            mVoiceRecognize = builder.setHost("apigwws.open.rokid.com")
                .setPort(443)
                .setBranch("/api")
                .setKey("your key")
                .setSecret("your secret")
                .setDeviceTypeId("your device_type_id")
                .setDeviceId("your device_id")
                .setCallback(this)
                .build();
    
            //mVoiceRecognize.control(VoiceRecognize.Action.ACTION_OPEN_MIC);
        }   
    
        @Override
        public void onVoiceEvent(VoiceRecognize.Event event, float sl, float energy) {
            Log.d(TAG, "onVoiceEvent    event " + event + ", sl " + sl + ", energy " + energy);
        }   
        
        @Override
        public void onIntermediateResult(String asr, boolean isFinal) {
            Log.d(TAG, "onIntermediateResult    asr " + asr);
        }   
        
        @Override
        public void onRecognizeResult(String nlp, String action) {
            Log.d(TAG, "onRecognizeResult   nlp " + nlp + ", action " + action);
        }   
        
        @Override
        public void onException(int errCode) {
            Log.d(TAG, "onException     errCode " + errCode);
        }   
    
        @Override
        public android.os.IBinder onBind(android.content.Intent intent) {
            return null;
        }   
    }

#####附件1：

>1、进入[Rokid开放平台](https://developer.rokid.com/#/)申请Rokid账号，已经有Rokid账号的同学可直接登录（但需进行部分信息补全）。
>
2、登录后点选「语音接入」进行设备认证信息申请。
>
3、具体做法：语音接入 > 创建新设备 > 填写设备名称 > 创建认证文件。之后您将获得：
>
account\_id、device\_type\_id、device\_id、secret、key



