
# 快速集成

## 集成步骤

### 下载SDK

  * 请通过 [Rokid SDK下载网站](https://developer-dev.rokid.com/tob2) ，根据网站提示进行配置，生成 SDK 后下载

###集成SDK
 ####下载sdk后，把.so文件放入androidstudio中app\src\main\jniLibs\armeabi-v7a\

 ####[](images/appkuanjia.png)

#### jar架包放入app\libs\目录下
	![](images/jarlib.png)
#### 配置文件放入\app\src\main\assets\configturen\
	![](images/configturen.png)
#### 配置权限
	![](images/quanxian.png)

### 集成注意事项

 * 目前Android电视前端语音识别部分仅支持32位armeabi-v7a so文件输出,64位支持正在开发中,敬请期待.

### 接口调用说明
* 请参考[Android电视方案接口调用说明](api_voicerecognize.md)



























