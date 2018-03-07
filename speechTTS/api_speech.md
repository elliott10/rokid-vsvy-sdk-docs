# 语音识别服务
## API 参考

### 1.SDK 初始化
**接口说明**

Rokid Speech 语音合成 SDK 初始化

**方法预览**

返回类型|方法|备注|
---|---|---|
void|prepare(PrepareOptions options)|使用PrepareOption 初始化|

**参数说明**

字段| 类型 |必须？| 描述
---|---|---|---|
options | PrepareOptions | 可选 |选项，详见PrepareOptions数据结构

**示例代码**

```java
//使用 PrepareOption 初始化
        Speech speech = new Speech();
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

关闭 Rokid Speech 语音识别服务

**方法预览**

返回类型|方法|备注|
---|---|---|
void|release()|Speech SDK关闭

**示例代码**

```java
	...
	speech.release();
```
### 3.文本识别

**接口说明**

Rokid 语音识别服务允许用户直接发送

~ | 名称 | 类型 | 描述
---|---|---|---
接口 | putText | | 发起文本speech
参数 | text | String | speech文本
参数 | cb | SpeechCallback | speech回调接口对象
返回值 | | int | speech id

~ | 名称 | 类型 | 描述
---|---|---|---
接口 | startVoice | | 发起语音speech
参数 | cb | SpeechCallback | speech回调接口对象
参数 | options | [VoiceOptions](#vo) | 当前语音speech的选项，详见[VoiceOptions](#vo)。此参数可不带
返回值 | | int | speech id

~ | 名称 | 类型 | 描述
---|---|---|---
接口 | putVoice | | 发送语音数据, 一次speech的语音数据可分多次发送
参数 | id | int | speech id
参数 | data | byte[] | 语音数据
返回值 | 无 | |

~ | 名称 | 类型 | 描述
---|---|---|---
接口 | endVoice | | 通知sdk语音数据发送完毕，结束speech
参数 | id | int | speech id
返回值 | 无 | |

~ | 名称 | 类型 | 描述
---|---|---|---
接口 | cancel | | 取消指定的speech请求
参数 | id | int | speech id
返回值 | 无 | |

~ | 名称 | 类型 | 描述
---|---|---|---
接口 | config | | 设置speech选项
参数 | options | [SpeechOptions](#so) | 详见[SpeechOptions](#so)
返回值 | 无 | |

## SpeechOptions

返回类型|方法|备注|
---|---|---|
void | set\_lang(String lang) | 设定文字语言。设定speech putText接口要发送的文本的语言; 影响语音识别结果'asr'的文本语言
void | set\_codec(String codec)| 设定语音编码。指定putVoice接口发送的语音编码格式
void | set\_vad\_mode(String mode)|设定语音起始结束检查在云端还是本地
void | set\_no\_nlp(boolean v)|设定是否需要服务端给出nlp结果
void | set\_no\_intermediate\_asr(boolean v)| 设定是否需要服务端给出中间asr结果

**set\_lang**

**参数说明**

字段| 类型 |必须？| 描述
---|---|---|---|
lang | String | 是 |限定值```zh```、```en```

**set\_codec**

**参数说明**

字段| 类型 |必须？| 描述
---|---|---|---|
codec | String | 是 |编码格式，限定值```pcm```、```opu```

**set\_vad\_mode**

**参数说明**

字段| 类型 |必须？| 描述
---|---|---|---|
mode | String | 是 |限定值```local```、 ```cloud```

**set\_no\_nlp**

**参数说明**

字段| 类型 |必须？| 描述
---|---|---|---|
v | boolean | 是 |

**set\_no\_intermediate\_asr**

**参数说明**

字段| 类型 |必须？| 描述
---|---|---|---|
v | boolean | 是 |

## 回调接口

### SpeechCallback

返回类型|方法|备注|
---|---|---|
void | onStart(int i) | speech结果开始返回
void | onIntermediateResult(int i,String s，String s1)| 给出当前已经转成语音的文字
void | onAsrComplete(int i,String s)|speech asr完整结果
void | onComplete(int i，String s,String s1)|speech最终结果
void | onCancel(int i)| speech被取消
void | onError(int id,int i1)| speech出错

**onStart(int id)**

**参数说明**

字段| 类型 | 描述
---|---|---|---|---
i| int  | 当前Speech 请求的id

**onIntermediateResult(int i,String s，String s1)**

**参数说明**

字段| 类型 | 描述
---|---|---|
id | int | speech id
s | String | 语音转文字中间结果
s1 | String | 激活结果

**onAsrComplete(int i,String s)**

**参数说明**

字段| 类型 | 描述
---|---|---|
i | int | 当前Speech 请求的id
s | String | 语音转文字完整结果

**onComplete(int i，String s,String s1)**

**参数说明**

字段| 类型 | 描述
---|---|---|
i | int |当前Speech 请求的id
s | String | 自然语义解析结果
s1 | String | rokid speech skill返回的结果

**onCancel(int i)**

**参数说明**

字段| 类型 | 描述
---|---|---|
id | int | 当前Speech 请求的id
**onError(int id,int i1)**

**参数说明**

字段| 类型 | 描述
---|---|---|
id | int |当前Speech 请求的id
err | int | 错误码

## 数据结构

### Speech.VoiceOptions

名称 | 类型 | 描述
---|---|---
stack | String |
voice\_trigger | String | 激活词
trigger\_start | int | 语音数据中激活词的开始位置
trigger\_length | int | 激活词语音数据长度
skill\_options | String |

### PrepareOptions
名称 | 类型 | 描述
---|---|---
host | String | tts服务host
port | int | tts服务port
branch | String | tts服务url path
key | String | tts服务认证key
device\_type\_id | String | 设备类型，用于tts服务认证
secret | String | 用于tts服务认证
device\_id | String | 设备id，用于tts服务认证


