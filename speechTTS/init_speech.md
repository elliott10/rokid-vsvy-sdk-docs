###  语音识别服务集成

用户需要在使用语音识别服务之前，调用上下代码来进行初始化

首先实例化语音识别服务对象

```java
        Speech speech = new Speech();
```
传入之前获取的相关秘钥，以及相关配置信息

```java
        PrepareOptions prepareOptions = new PrepareOptions();
        prepareOptions.host = "apigwws.open.rokid.com";
        prepareOptions.port = 443;
        prepareOptions.branch = "/api";
        //key
        prepareOptions.key = "";
        //device_type_id
        prepareOptions.device_type_id = "";
        //secret
        prepareOptions.secret = "";
        //device_id
        prepareOptions.device_id = "";
        
        speech.prepare(prepareOptions);

```

```java
        // 修改音频编码格式及语言，其它选项不变
        SpeechOptions opts = new SpeechOptions();
        opts.set_codec("opu");
        opts.set_lang("zh");
        speech.config(opts);
```

以上为初始化步骤，如需验证请参考下述代码

```java
speech.putText("你好若琪", new SpeechCallback() {
            @Override
            public void onStart(int i) {
                LogUtil.d("onStart " + i);
            }

            @Override
            public void onIntermediateResult(int i, String s, String s1) {
                LogUtil.d("onIntermediateResult " + i + " " + s + " " + s1);
            }

            @Override
            public void onAsrComplete(int i, String s) {
                LogUtil.d("onAsrComplete " + i + " " + s);
            }

            @Override
            public void onComplete(int i, final String s, final String s1) {
                LogUtil.d("onComplete " + s + " " + s1);
                //需要在主线程更新ui
             
            }

            @Override
            public void onCancel(int i) {
                LogUtil.d("onCancel " + i);
            }

            @Override
            public void onError(int i, int i1) {
                LogUtil.d("onError " + i + " " + i1);
            }
        });
```


