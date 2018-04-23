## mic_array实现简要说明
### mic_array要实现的功能
- mic_array模块要实现麦克风阵列的打开/读取数据功能,然后turenproc进程会根据标准的 ```android hw_module_t``` 的```open/start_stream/read_stream```  等方法读取mic阵列的数据,送给前端算法,进行数据处理.

### mic_array要实现的接口
```
    int (*get_stream_buff_size) (struct mic_array_device_t *dev);
    int (*start_stream) (struct mic_array_device_t *dev);
    int (*stop_stream) (struct mic_array_device_t *dev);
    int (*finish_stream) (struct mic_array_device_t * dev);
    int (*resume_stream) (struct mic_array_device_t *dev);
    int (*read_stream) (struct mic_array_device_t *dev, char *buff, unsigned int frame_cnt);
    int (*config_stream) (struct mic_array_device_t *dev, int cmd, char *cmd_buff);
```
- 如上接口均为audio hal层标准命名接口(可参考 ```mic_array.h``` 定义),需要各个厂商根据自己硬件麦克风阵列的打开以及读取方式,实现对应接口

### mic_array 模块编译参考
```
LOCAL_PATH := $(call my-dir)
include $(CLEAR_VARS)
LOCAL_SRC_FILES := mic_array.c
LOCAL_MODULE_PATH := $(TARGET_OUT_SHARED_LIBRARIES)/hw
LOCAL_MODULE := mic_array.$(TARGET_DEVICE)
LOCAL_MODULE_TAGS := optional
LOCAL_C_INCLUDES += hardware/libhardware \
	external/tinyalsa/include
LOCAL_SHARED_LIBRARIES := liblog libcutils libtinyalsa
LOCAL_MODULE_TARGET_ARCH := arm
include $(BUILD_SHARED_LIBRARY)
```
- 参考如上 ```Android.mk``` 的编写方式,在android源码中编译时,会将 ```mic_array``` 模块编译为 ```mic_array.{TARGET_DEVICE}.so``` ,生成目录为 ```out/target/product/{TARGET_DEVICE}/system/lib/hw/``` 

### mic_array 几个主要的参数
```
static struct pcm_config pcm_config_in = {
    .channels = 8,
    .rate = 48000,
    .period_size = 1024,
    .period_count = 8,
    .format = PCM_FORMAT_S32_LE,
};
```
- 配置硬件麦克风阵列的录音参数
 - ```channels``` 为麦克风声道数,表示录音时有几路输入
 - ```rate``` 为麦克风录音时的采样率，即每秒的采样次数，针对帧而言,目前支持最少16000
 - ```period_size``` 每次硬件中断处理音频数据的帧数
 - ```period_count``` 处理完一个buffer数据所需的硬件中断次数
 - ``` format``` 样本长度，音频数据最基本的单位,比如PCM_FORMAT_S32_LE/PCM_FORMAT_S24_LE
 - 麦克风阵列每秒读取的数据大小取决于 ```channels``` / ```rate```/```format```/,比如```format```为```PCM_FORMAT_S32_LE(4 byte)```,```channels``` 为 8 ,```rate``` 为 48000,时,麦克风阵列每秒读取数据大小为 ```48000*8*4 = 1536000(byte)```, 麦克风阵列每一次读取数据的大小为 ```period_count``` * ```period_size``` ,每次读取的数据都是分帧组合,每一帧(```frame_size```)大小取决于```channel``` 以及 ```format```,比如```channel```为 8,```format``` 为 ```PCM_FORMAT_S32_LE```时,每一帧的大小则为 ```8*4 = 32(byte)```,每一次读取的数据帧数 ```frame_cnt``` 即```get_stream_buff_size```方法获取的数据大小为```period_count```*```period_size```/```frame_size```, 此大小建议根据麦克风每秒输入数据总大小进行配置,以```10ms/次```的消费速度消费数据.同时每次读取的数据需要根据```format```和 ```channels```的配置,按照```channels```的顺序进行排列.比如 ```format``` 为 ```PCM_FORMAT_S32_LE```,```channels``` 为 8,则每帧数据格式如下
```
|32byte(mic0)|32byte(mic1)|32byte(mic2)|32byte(mic3)|32byte(mic4)|32byte(mic5)|32byte(mic6)|32byte(mic7)|32byte(mic0)|32byte(mic1)|32byte(mic2)|32byte(mic3)|32byte(mic4)|32byte(mic5)|32byte(mic6)|32byte(mic7)|.|.|.|.|.|.|.|.|
```


```
static struct hw_module_methods_t mic_array_module_methods = {
    .open = mic_array_device_open,
};

struct mic_array_module_t HAL_MODULE_INFO_SYM = {
    .common = {
        .tag = HARDWARE_MODULE_TAG,
        .version_major = 1,
        .version_minor = 0,
        .id = "mic_array",
        .name = "mic_array",
        .author = "xxxxxxxx",
        .methods = &mic_array_module_methods,
    },
};
```
- 定义android标准的```HAL_MODULE_INFO_SYM```,其中 ```id``` 和 ```name``` 必须使用 ```mic_array``` ,否则turenproc进程在运行时会提示```[Error] Mic Array init (not found mic_array.xxx.so) : -2``` 