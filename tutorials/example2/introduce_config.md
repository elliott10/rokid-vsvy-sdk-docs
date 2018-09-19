#### 前端配置文件配置
- 配置 ```ctc.xxx.cfg``` ,其中 ```xxx``` 值为 ```android``` 编译源码是的```${TARGET_DEVICE}```的值
```
phonetable=phonetable
ctc=rasr.emb.ini
words=ruoqi,meishile
asr.line.num=4
bf.num=12
```
 - phonetable: 音素表配置
 - ctc: 激活模型配置
 - words: 激活词配置,如上两个分别对应```workdir_asr_cn```下的 ```word.ruoqi.cfg``` 和 ```word.meishile.cfg```
 
- 配置 ```device.xxx.cfg``` , 其中 ```xxx``` 值为android编译源码是的 ```${TARGET_DEVICE}``` 的值
  - audio.rate=48000 // 采样率
  - audio.type=int // 采样位(short/int/float)
  - mic.num=8  // 麦克风个数,根据实际数量配置
  - in.mics =0,1,2,3,6,7 // 麦克风个数,根据实际输入通道进行配置
  - rs.mics =0,1,2,3,4,5 // 重采样通道,根据实际输入通道进行配置
  - aec.mics=0,1,2,3 // aec声道,根据实际输入通道进行配置
  - ref.mics=4,5 // 参考声道,根据实际输入通道进行配置
  - in.mics.big.0 =0.5 // 0声道采样值放大系数,如无此参数,则表示不放大,默认可以先不配置
  - in.mics.big.1 =0.5 // 1声道采样值放大系数,如无此参数,则表示不放大,默认可以先不配置
  - in.mics.big.2 =0.5 // 2声道采样值放大系数,如无此参数,则表示不放大,默认可以先不配置
  - in.mics.big.3 =0.5 // 3声道采样值放大系数,如无此参数,则表示不放大,默认可以先不配置
  - in.mics.big.4 =0.5 // 4声道采样值放大系数,如无此参数,则表示不放大,默认可以先不配置
  - in.mics.big.5 =0.5 // 5声道采样值放大系数,如无此参数,则表示不放大,默认可以先不配置
  - in.mics.big.6 =0.5 // 6声道采样值放大系数,如无此参数,则表示不放大,默认可以先不配置
  - in.mics.big.7 =0.5 // 7声道采样值放大系数,如无此参数,则表示不放大,默认可以先不配置
  - bf.mics=0,1,2,3  //波束声道道,根据实际输入通道进行配置
  - mic.pos.0= 0.03000000, 0.00000000, 0.00000000 // 0mic 坐标位置
  - mic.pos.1= 0.00000000, 0.03000000, 0.00000000 // 1mic 坐标位置
  - mic.pos.2= -0.03000000, 0.00000000, 0.00000000 // 2mic 坐标位置
  - mic.pos.3= 0.00000000, -0.03000000, 0.00000000 // 3mic 坐标位置
  - mic.pos.4= 0,0,0 // 4mic 坐标位置
  - mic.pos.5= 0,0,0 // 5mic 坐标位置
  - mic.pos.6= 0,0,0 // 6mic 坐标位置
  - mic.pos.7= 0,0,0 // 7mic 坐标位置
  - mic.delay=0,0,0,0,0,0,0,0  //ref通道不同时延时配置,默认都为0
  - codec=true // 是否opu编码后上传给服务端,默认需要
  - light.angle0=180 // 灯光起始角度
  - light.angle.mul=1 // 灯光角度偏移系数, 1/-1, 顺时针/逆时针

- 将配置OK的前端配置文件放入 ```SDK``` 的 ```config/workdir_asr_cn/```目录下


