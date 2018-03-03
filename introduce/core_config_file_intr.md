### 相关配置文件简介

在介绍开始前，我们将用表格的形式列举出相关配置文件的文件名，以及应该存在的位置，以便用户参考

| 配置名称  | 类型  | 位置 |
|:------------- |:---------------:| -------------:|
| `openvoice_profile.json`| 文件 | `/system/etc` |
| `exec_config.json`| 文件 | `/system/etc` |
| `workdir_cn`| 文件夹 |`/system`|
|`libmic_array.so`|文件|`/system/lib`|


#### openvoice_proflie.json
该文件是语音接的配置，使你的设备获得 Rokid 语音服务。
#### exec_config.json
该文件为 SDK 中语音识别结果分发的配置文件，语音识别结果返回后会根据改配置文件中的参数跳转至指定技能
#### workdir_cn
该文件夹下面的文件为用于语音识别的模型库。