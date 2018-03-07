# 语音合成服务
## API 参考

### 1.SDK 初始化
**接口说明**

Rokid TTS 语音合成 SDK 初始化

**方法预览**

返回类型|方法|备注|
---|---|---|
void|prepare(PrepareOptions options)|使用PrepareOption 初始化|
void|prepare(String configFile)|使用配置文件初始化|
void|prepare(InputStream is)|使用流初始化|

**参数说明**

字段| 类型 |必须？| 描述
---|---|---|---|---
options | [PrepareOptions](#po) | 可选 |选项，详见[PrepareOptions](#po)数据结构
configFile | String | 可选 |配置文件路径名。文件内容详见[json格式配置字串](#jsonconf)
 is | InputStream | 可选 |数据流，流内容详见[json格式配置字串](#jsonconf)
 
**示例代码**

```java
//使用 PrepareOption 初始化
		PrepareOptions popts = new PrepareOptions();
        popts.host = "apigwws.open.rokid.com";
        popts.port = 443;
        popts.branch = "/api";
        popts.key = "";
        popts.device_type_id = "";
        popts.secret = "";
        popts.device_id ="";
        tts.prepare(popts);
``` 

### 2.SDK 关闭

**接口说明**

关闭 Rokid TTS 语音合成服务

**方法预览**

返回类型|方法|备注|
---|---|---|
void|release()|TTS SDK关闭

**示例代码**

```java
	...
	tts.release();
```

### 3.文字转语音

**接口说明**

发起文字转语音请求

**方法预览**

返回类型|方法|备注|
---|---|---|
int|speak(String s , TtsCallback callback)|发起文字转语音请求

**参数说明**

字段| 类型 |必须？| 描述
---|---|---|---|---
s| String  | 必须 | 要朗读的文本
callback | TtsCallback | 必须 | 回调接口

**返回值**

 类型 | 描述
---|---|---|
int|成功将文本加入待处理队列，返回id。失败返回-1

**示例代码**

```java
	int id = 0;
	id = tts.speak(s,new TtsCallback() {
                    // 在这里实现回调接口 onStart, onVoice等
                    // 在onVoice中得到语音数据，调用播放器播放
                    @Override
                    public void onStart(int i) {

                    }

                    @Override
                    public void onText(int i, String s) {

                    }

                    public void onVoice(int id, byte[] data) {
                    	...doSth
                    }

                    @Override
                    public void onCancel(int i) {

                    }

                    @Override
                    public void onComplete(int i) {

                    }

                    @Override
                    public void onError(int i, int i1) {

                    }
                });
```

### 4.取消文字转语音请求

**接口说明**

取消文字转语音请求

**方法预览**

返回类型|方法|备注|
---|---|---|
void|cancel(int id)|取消文字转语音请求

**参数说明**

字段| 类型 |必须？| 描述
---|---|---|---|---
id| String  | 必须 | 此前调用speak返回的id
callback | TtsCallback | 必须 | 回调接口

**示例代码**

```java
	...
	tts.cancel(id) //此前调用speak返回的id
```

### 5. 修改TTS配置选项

**接口说明**

修改TTS配置选项

**方法预览**

返回类型|方法|备注|
---|---|---|
void|config([TtsOptions](#to) options)| TTS的配置选项，详见[TtsOptions](#to)数据结构

**参数说明**

字段| 类型 |必须？| 描述
---|---|---|---|---
options | [TtsOptions](#to) | 是 |TTS的配置选项，详见[TtsOptions](#to)数据结构

**示例代码**

```java
	
	
	
```

## 回调接口

### TtsCallback

返回类型|方法|备注|
---|---|---|
void | onStart(int i) | 开始接收语音数据流
void | onText(int i,String s)| 给出当前已经转成语音的文字
void | onVoice(int id,byte[] data)|语音数据流
void | onCancel(int i)|语音转文字已经取消
void | onComplete(int i)| 语音数据已经全部给出
void | onError(int id,int i1)| 语音转文字出错

**onStart**

**参数说明**

字段| 类型 | 描述
---|---|---|---|---
i| int  |成功将文本加入待处理队列,TTS Speak返回的id

**onText**

字段| 类型 | 描述
---|---|---|---|---
i| int  |TTS Speak返回的id
s|String| 当前已经转成语音的文字

**onVoice**

字段| 类型 | 描述
---|---|---|---|---
data | byte[] | 语音数据，根据[TtsOptions](#to)决定编码格式

**onCancel**

字段| 类型 | 描述
---|---|---|---|---
 id | int |TTS Speak返回的id

**onComplete**

字段| 类型 | 描述
---|---|---|
 id | int |TTS Speak返回的id

**onError**

字段| 类型 | 描述
---|---|---|---|---
id | int |TTS Speak返回的id
err | int | [错误码](#errcode)
返回值 | 无 | |
