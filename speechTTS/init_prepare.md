# 集成前准备

## 复制文件

将```rokid_speech.jar```复制到 Android 工程下的 ```libs``` 文件夹中，并设置为工程的依赖库

将二进制库文件复制进工程目录下的 ```app/src/main/jniLibs``` 下

## 添加权限

```xml
    <!--网络访问权限-->
    <uses-permission android:name="android.permission.INTERNET" />
```




