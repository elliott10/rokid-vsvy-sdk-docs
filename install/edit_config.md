### openvoice_proflie.json
#### 具体做法：
首先需要登录 Rokid 开放平台，之后按照如下步骤执行：

1. 进入 Rokid 开放平台 申请 Rokid 账号，若您已经申请了 Rokid 账号，可直接登录(但需进行部分信息补全)。
1. 登录后点选「语音接入」进行设备认证信息申请。
1. 具体做法：语音接入 >> 创建新设备 >> 填写设备名称 >> 创建认证文件。之后您将获得：

        account_id、device_type_id、secret、key

1. 创建openvoice_profile文件并将将获得的信息填写到openvoice_proflie.json中
`vim openvoice_proflie.json`

```
{
     "host": "apigwws.open.rokid.com",
     "event_req_host": "apigwrest.open.rokid.com",
     "port": "443",
     "branch": "/api",
     "key": "your key",
     "device_type_id": "your device_type_id",
     "device_id": "your account_id",
     "secret": "your secret",
     "api_version":"1",
     "lang": "zh",
     "codec": "opu",
     "vad_mode": "cloud",
     "vend_timeout": 500
 }
```

### blackSiren.json

1. 创建文件

`vim blackSiren.json`

2. 配置方法
[简单易懂的Blackserion配置文档](./简单易懂的Blackserion配置文档.pdf
)

#### 文件内容如下
```
{
    "basic_config": {
        "mic_num":8,
        "mic_channel_num":8,
        "mic_sample_rate":48000,
        "mic_audio_byte":4,
        "mic_frame_length":10,
        "siren_ipc":"channel",
        "siren_channel_rmem":4194304,
        "siren_channel_wmem":6291456,
        "siren_input_err_retry_num":5,
        "siren_input_err_retry_timeout":100,
        "siren_monitor_udp_port":65456
    },
    "alg_config": {
        "alg_use_legacy_config_file":true,
        "alg_legacy_config_file_path":"/system/workdir_cn",
        "alg_lan":"zh",
        "alg_rs_mics":[0,1,2,3,6,7],
        "alg_aec":true,
        "alg_aec_mics":[0,1,2,3],
        "alg_aec_ref_mics":[6,7],
        "alg_aec_shield":200.0,
        "alg_aec_aff_cpus":[3],
        "alg_aec_mat_aff_cpus":[2,3],
        "alg_raw_stream_sl_direction":180.0,
        "alg_raw_stream_bf":true,
        "alg_raw_stream_agc":true,
        "alg_vt_enable":true,
				"alg_rs_enable":true,
        "alg_vad_enable":false,
        "alg_vad_mics":[3],
        "alg_vad_baserange":1.25,
        "alg_vad_dynrange_min":3.5,
        "alg_vad_dynrange_max":6.0,
        "alg_need_i2s_delay_mics":[1,3,5,7],
        "alg_i2s_delay_mics":[0.00001041, 0.00001041, 0.00001041, 0.00001041],
        "alg_mic_pos":[[0.03000000, 0.00000000, 0.00000000],
			[0.00000000, 0.03000000, 0.00000000],
                       	[-0.03000000, 0.00000000, 0.00000000],
                       	[0.00000000, -0.03000000, 0.00000000],
	               	[0.0, 0.0, 0.0],
	                [0.0, 0.0, 0.0],
	                [0.0, 0.0, 0.0],
	                [0.0, 0.0, 0.0]],
            "alg_sl_mics":[0,1,2,3],
            "alg_bf_mics":[0,1,2,3],
            "alg_opus_compress":true,
            "alg_vt_phomod":"/system/workdir_cn/phonetable",
            "alg_vt_dnnmod":"/system/workdir_cn/final.svd.mod",
            "alg_def_vt":[
                {
                    "vt_type":1,
                    "vt_word":"若琪",
                    "vt_phone":"r|1|r_B|1_B|# w o4|o4_E|## q|q_B|# i2|i2_E|##",
                    "vt_block_avg_score":4.2,
                    "vt_block_min_score":2.7,
                    "vt_left_check":true,
                    "vt_right_check":true,
                    "vt_remote_check_with_aec":true,
                    "vt_remote_check_without_aec":true,
                    "vt_local_classify_check":true,
                    "vt_classify_shield":-0.3,
                    "vt_nnet_path":"/system/workdir_cn/final.ruoqi.mod"
                },
                {
                    "vt_type":1,
                    "vt_word":"小兴小兴",
                    "vt_phone":"x|x_B|# y a3 W|W_E|## x|x_B|# i1 NG|NG_E|## x|x_B|# y a3 W|W_E|## x|x_B|# i1 NG|NG_E|##",
                    "vt_block_avg_score":4.2,
                    "vt_block_min_score":2.7,
                    "vt_left_check":true,
                    "vt_right_check":true,
                    "vt_remote_check_with_aec":true,
                    "vt_remote_check_without_aec":true,
                    "vt_local_classify_check":false,
                    "vt_classify_shield":-0.3,
                    "vt_nnet_path":""
                },
                {
                    "vt_type":2,
                    "vt_word":"没事了",
                    "vt_phone":"m|m_B|# E2 Y|Y_E|## sh|s|sh_E|s_E|# I4|IH4|I4_E|IH4_E|## l|l_B|# e3|a3|e3_E|a3_E|##",
                    "vt_block_avg_score":4.7,
                    "vt_block_min_score":3.2,
                    "vt_left_check":true,
                    "vt_right_check":false,
                    "vt_remote_check_with_aec":false,
                    "vt_remote_check_without_aec":false,
                    "vt_local_classify_check":false,
                    "vt_classify_shield":-0.3,
                    "vt_nnet_path":""
                }
            ],
            "alg_rs_delay_on_left_right_channel":true,
            "raw_stream_channel_num":1,
            "raw_stream_sample_rate":16000,
            "raw_stream_byte":2
    },
    "debug_config": {
        "debug_mic_array_record":false,
        "debug_pre_result_record":false,
        "debug_proc_result_record":false,
        "debug_rs_record":false,
        "debug_aec_record":false,
        "debug_bf_record":false,
        "debug_bf_raw_record":false,
        "debug_vad_record":false,
        "debug_opu_record":false,
        "debug_record_path":"/data/blacksiren"
    }
}
```
### exec_config.json

1.创建文件
`vim exec_config.json`
#### 文件内容如下
>可以根据自己开发的应用配置：native是本地应用，clound是云应用

```
{
	"cloud": [
		{
			"action": "cloudengine",
			"type": "service"
		},
		{
			"action": "com.rokid.example.RKVoiceEventActivity",
			"type": "activity"
		}
	],
	"native": [
		{
			"action": "com.rokid.example.RKVoiceEventActivity",
			"type": "activity"
		}
	],
	"exit": [
		{
			"action": "cloudengine",
			"type": "service"
		},
		{
			"action": "com.rokid.example.RKVoiceEventService",
			"type": "service"
		}
	],
	"exception": [
		{
			"action": "com.rokid.example.RKVoiceEventService",
			"type": "service"
		}
	],
	"other": [
		{
			"action": "com.rokid.example.RKVoiceEventService",
			"type": "service"
		}
	]
}

```