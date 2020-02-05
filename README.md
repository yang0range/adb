## ADB
ADB全称Android Debug Bridge。  
ADB是一种功能多样的命令行工具，起到了调试桥的作用，可以用来操作Android设备。  
ADB是Android开发/测试人员强大的工具。  

可以说，ADB对我们Android的开发至关重要，深入的了解常用的命令和作用就显得至关重要了

ADB使一种客户端-服务器程序，包括以下三个组件：
- **客户端**：用于发送命令，客户端在开发计算机上运行，通过发出adb命令从命令行终端调用客户端。
- **守护进程**：在设备上运行命令，守护进程在每个设备上作为后太进程运行。
- **服务器**：管理客户端和守护进程之间的通信，服务器在开发计算机上作为后台进程运行。

adb包含在Android SDK平台工具软件包当中，如何配置环境变量网上有太多的教程，我们就不赘述了。

## ADB常用命令

环境变量配置完之后，我们输入adb，就会出现以下的一下命令提示。
![image](EDBA01D837A644D8AA4752863FF4B41A)
除了这个截图，后面还有很多的命令，接下来对我们常用的命令行进行一下详细的介绍。
看目录我们可以知道，ADB分为全局命令、常规命令、网络命令、文件传输命令、
应用安装命令、备份和恢复命令、调试命令、安全命令、脚本命令、内部调试命令、Shell命令。这几种命令，对于每一种命令，官网上都有详细的解释
[https://developer.android.google.cn/studio/command-line/adb#issuingcommands](https://developer.android.google.cn/studio/command-line/adb#issuingcommands)

接下来，对于常用的一些命令，我着重的介绍一下。

### ADB全局选项

全局选项 | 说明
---|---
-a | 在所有网络接口上监听，而非只在localhost上监听。
-d | 将adb命令发送到唯一连接的USB设备。如果连接了多个USB设备，则返回错误。
-e | 将adb命令发送到唯一运行的模拟器。如果有多个模拟器在运行，则返回错误。
-s  serial_number | 将adb命令发送到以其adb分配的序列号命名的特定设备（例如“emulator-5556”）。替换存储在 $ANDROID_SERIAL 环境变量中的序列号值。
-H server| adb服务器主机的名称。默认值为localhost。
-P port | adb服务端口号。默认值为5037。
-L socket | 在提供的adb socket服务器的监听。默认值为tcp:localhost:5037。


#### 启动/停止 服务
启动adb service命令:  
**adb start-server**  
但是，一般情况下，我们无需手动调用这个命令，在运行的adb命令时候发现adb service没用启动的时候才会调用。

停止 adb service命令：  
**adb kill-server**

### 常规命令

常规命令 | 说明
---|---
devices [-l]  | 输出所有的设备列表。-l 选项用于包含设备的描述
help | 输出支持的adb命令及其描述的列表
version | 输出adb版本号

#### 查看应用列表
查看应用列表的的命令是  
adb shell pm list packages   
具体的内容包括

参数 | 显示列表
---|---
无 | 所有应用
-f | 显示应用关联的apk文件
-d | 只显示disabled的应用
-e | 只显示enable的应用
-s | 只显示系统应
-3 | 只显示第三方应用
-i | 显示应用的installer
-u | 包含已卸载应用
-<FILTER> | 包名包含<FILTER>字符串

#### 安装APK
**adb install <apk file>**  
常见参数及含义

参数 | 含义
---|---
-r | 允许覆盖安装
-s | 将应用安装到sdcard
-d | 允许降级覆盖安装  

#### 卸载应用

**adb unstall [-k] <packagename>**  
其中 <packagename> 表示应用的包名，-k参数可选，表示卸载应用但是保留数据和缓存目录。

#### 清除应用数据与缓存

**adb shell pm clear <packagename>**
<packagename>表示应用包名

#### 查看日志

[adb] logcat [<option>] ... [<filter-spec>] ...常用用法列举如下：  

**1. 按级别过滤日志**  
Android 的日志分为如下几个级别：   
V —— Verbose（最低，输出得最多）   
D —— Debug   
I —— Info  
W —— Warning  
E —— Error  
F —— Fatal  
S —— Silent（最高，啥也不输出）  

按某级别过滤日志则会将该级别及以上的日志输出。
比如，命令：
adb logcat *:W会将 Warning、Error、Fatal 和 Silent 日志输出。

**2. 按 tag 和级别过滤日志**  
比如，命令：  

adb logcat  MyApp:D *:S  

表示输出   
tag ActivityManager 的 Info 以上级别日志。

#### 打开指定Activity

adb shell am start [options] <INTENT>  
  例如：    
adb shell am start -n com.tencent.mm/.ui.LauncherUI

#### 查看bug报告

adb bugreport

## 参考连接

[https://developer.android.google.cn/studio/command-line/adb#issuingcommands](https://developer.android.google.cn/studio/command-line/adb#issuingcommands)  

[https://segmentfault.com/a/1190000006729971#item-4](https://segmentfault.com/a/1190000006729971#item-4)




