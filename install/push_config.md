### 第一步 推送相关配置文件

>注意！！！ 配置文件需要推送的目录，一般情况下均为只读
>可使用 `adb root`、`adb remount` 两个命令来更改状态
>用户可使用`adb push`命令来推送相关文件

下表列举了需要推送的文件以及指定路径

| 配置名称  | 类型  | 位置 |
|:------------- |:---------------:| -------------:|
| `openvoice_profile.json`| 文件 | `/system/etc` |
| `blacksiren.json`| 文件 | `/system/etc` |
| `exec_config.json`| 文件 | `/system/etc` |
|`libmic_array.so`|文件|`/system/lib`|
| `workdir_cn`| 文件夹 |`/system`|