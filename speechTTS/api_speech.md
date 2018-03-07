


**回调接口**



### OpusPlayer接口

用于帮助播放opu2格式tts音频数据的工具类

~ | 名称 | 类型 | 描述
---|---|---|---
接口 | play | | 播放opu2格式音频数据
参数 | data | byte[] | 音频数据


### Speech接口定义

**调用接口**
~ | 名称 | 类型 | 描述
---|---|---|---
接口 | prepare | | speech sdk初始化
参数 | options | [PrepareOptions](#po) | 选项，详见[PrepareOptions](#po)数据结构
返回值 | 无 | |

~ | 名称 | 类型 | 描述
---|---|---|---
接口 | release | | speech sdk关闭
参数 | 无 | |
返回值 | 无 | |

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

**回调接口**

~ | 名称 | 类型 | 描述
---|---|---|---
接口 | onStart | | speech结果开始返回
参数 | id | int | speech id

~ | 名称 | 类型 | 描述
---|---|---|---
接口 | onIntermediateResult | | speech中间结果。可能回调多次
参数 | id | int | speech id
参数 | asr | String | 语音转文字中间结果
参数 | extra | String | 激活结果

~ | 名称 | 类型 | 描述
---|---|---|---
接口 | onAsrComplete | | speech asr完整结果
参数 | id | int | speech id
参数 | asr | String | 语音转文字完整结果

~ | 名称 | 类型 | 描述
---|---|---|---
接口 | onComplete | | speech最终结果
参数 | id | int | speech id
参数 | nlp | String | 自然语义解析结果
参数 | action | String | rokid speech skill返回的结果

~ | 名称 | 类型 | 描述
---|---|---|---
接口 | onCancel | | speech被取消
参数 | id | int | speech id

~ | 名称 | 类型 | 描述
---|---|---|---
接口 | onError | | speech出错
参数 | id | int | speech id
参数 | err | int | [错误码](#errcode)

### 数据结构

#### <a id="po"></a>PrepareOptions

名称 | 类型 | 描述
---|---|---
host | String | tts服务host
port | int | tts服务port
branch | String | tts服务url path
key | String | tts服务认证key
device\_type\_id | String | 设备类型，用于tts服务认证
secret | String | 用于tts服务认证
device\_id | String | 设备id，用于tts服务认证

#### <a id="to"></a>TtsOptions


#### <a id="so"></a>SpeechOptions

使用set\_xxx接口设定选项值，未设定的值将不会更改旧有的设定值

~ | 名称 | 类型 | 描述
---|---|---|---
接口 | set\_lang | | 设定文字语言。设定speech putText接口要发送的文本的语言; 影响语音识别结果'asr'的文本语言
参数 | lang | String | 限定值"zh" "en"

~ | 名称 | 类型 | 描述
---|---|---|---
接口 | set\_codec | | 设定语音编码。指定putVoice接口发送的语音编码格式
参数 | codec | String | 限定值"pcm" "opu"

~ | 名称 | 类型 | 描述
---|---|---|---
接口 | set\_vad\_mode | | 设定语音起始结束检查在云端还是本地
参数 | mode | String | 限定值"local" "cloud"

~ | 名称 | 类型 | 描述
---|---|---|---
接口 | set\_no\_nlp | | 设定是否需要服务端给出nlp结果
参数 | v | boolean |

~ | 名称 | 类型 | 描述
---|---|---|---
接口 | set\_no\_intermediate\_asr | | 设定是否需要服务端给出中间asr结果
参数 | v | boolean |

#### <a id="vo"></a>VoiceOptions

名称 | 类型 | 描述
---|---|---
stack | String |
voice\_trigger | String | 激活词
trigger\_start | int | 语音数据中激活词的开始位置
trigger\_length | int | 激活词语音数据长度
skill\_options | String |

#### <a id="jsonconf"></a>Json格式配置字串

key | 描述
--- | ---
host | 服务器主机名 一般使用apigwws.open.rokid.com
port | 服务器端口 目前为443
branch | 服务器功能选择分支 固定为/api
key | 用于服务登录认证　
device\_type\_id | 用于服务登录认证
secret | 用于服务登录认证
device\_id | 设备名，用于服务登录
codec | 语音编码格式:<br>speech服务可选项"pcm" "opu"<br>tts服务可选项 "pcm" "opu2" "mp3"
speech服务专有配置 | ...
lang | 语音语言: "zh"或"en"
vad\_mode | 判断语音结束算法部署位置:<br>"cloud" 云端运行算法，准备确率高<br>"local" 本地运行算法
vend\_timeout | 用于判断语音结束的参数，一般不需设置，使用默认值
no\_nlp | true或false: 是否接收nlp/action结果
no\_intermediate\_asr | true或false: 是否接收asr中间识别结果
tts服务专有配置 | ...
declaimer | 语音播报员设置<br>目前只有一个播报员，默认名"zh"。未来将扩展多个播报员。

上面列出的key值在配置字串中都是可选项，如不配置则使用缺省值

配置字串示例

```
{
	'host': 'apigwws.open.rokid.com',
	'port': 443,
	'branch': '/api',
	'key': '用于服务认证的key',
	'device_type_id': '用于服务认证的device_type_id',
	'secret': '用于服务认证的secret',
	'device_id': '设备id 一般使用设备sn'
}
```