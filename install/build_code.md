### 编译
>注：sdkmanager的运行需要openjdk1.8环境，但我们源码的编译只需要openjdk1.7以上的环境。所有想要切回openjdk1.7以上的环境

>可以如图在配置文件注释掉你的1.8的版本
>
![](img/pic3.jpg)

```
cd <vsys_src>
. build/envsetup.sh
lunch
  lunch将列出三个选项如下：
  1. android6.0/7.0/7.1
  2. android4.4
  3. android5.0/5.1
  根据需要自行选择
make
```
> 编译后apk输出在 out/target/\<target_platform\>/目录下
> 注：\<target_platform\>为19/21/23。19对应android4.4，21对应android5.0/5.1，23对应android6.0/7.0/7.1