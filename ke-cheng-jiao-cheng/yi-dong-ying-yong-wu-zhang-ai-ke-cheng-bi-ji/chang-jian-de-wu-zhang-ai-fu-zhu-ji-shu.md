# 常见的无障碍辅助技术

辅助功能是指一类软硬件设备，它提供的特殊或增强功能，能够满足障碍用户的需求。iOS系统和Android系统的辅助功能分类略有不同，以下分开介绍。



## 01 iOS辅助功能 <a href="#kxkz1" id="kxkz1"></a>

### 视力 <a href="#pv6hk" id="pv6hk"></a>

旁白功能

朗读内容

放大器

文字大小

显示设置

缩放

口述影像



### 听力 <a href="#jvx64" id="jvx64"></a>

对话增强

助听设备

耳机调节

声音识别

FaceTime通话

实时收听

知觉提醒



### 肢体活动能力 <a href="#izvir" id="izvir"></a>

语音控制

切换控制

辅助触控

备选输入

轻点背面

Siri

触控调节



### 认知能力 <a href="#mdsfo" id="mdsfo"></a>

背景音

朗读内容

Safari浏览器的阅读器

引导式访问

面容识别

iCloud钥匙串

听写



更多详情可以在苹果设备和[苹果官网](https://apple.com.cn/accessibility)查看。



## 02 Android辅助功能 <a href="#ttsoa" id="ttsoa"></a>

### 视觉 <a href="#wgmmp" id="wgmmp"></a>

TalkBack

Lookout

放大功能

颜色校正

显示大小和字体大小

随选朗读



### 听觉 <a href="#qylbc" id="qylbc"></a>

实时字幕

声音增强器

助听器支持

实时转写

声音通知

实时信息（RTT )



### 移动 <a href="#gakig" id="gakig"></a>

开关控制

voice Access

无障碍功能菜单

操作区块



安卓不是没有认知相关的辅助功能，而是因为划分的方式和ios平台有区别。更多详情可以在[谷歌帮助中心](https://support.google.com/accessibility/android?sjid=6273537404693027782-NA#topic=6007234)查看。



## 03 常见的辅助功能 <a href="#dv4d4" id="dv4d4"></a>

### 视觉障碍 <a href="#rslwf" id="rslwf"></a>

<mark style="color:blue;">屏幕阅读器</mark>

将屏幕上的内容以语音的形式告知用户。对应iOS的旁白、Android的TalkBack。



<mark style="color:blue;">放大</mark>

对应iOS的缩放、Android的放大功能。



<mark style="color:blue;">字体大小</mark>

对应iOS的文字大小、Android的字体大小。



<mark style="color:blue;">朗读内容</mark>

把整个屏幕上的内容都大声朗读。对应iOS的朗读内容、Android的随选朗读。



### 听力障碍 <a href="#lhugm" id="lhugm"></a>

<mark style="color:blue;">字幕</mark>

实时字幕（Android系统独有）

隐藏式字幕（iOS系统独有）：只针对一些带有隐藏字幕的媒体内容。



<mark style="color:blue;">声音识别</mark>

iOS的，持续听取某些声音（比如婴儿哭声、门铃、鸣笛声）并在识别出这些声音时通知给用户。



<mark style="color:blue;">声音增强器</mark>

Android的，放大手机音量，滤除背景噪声，并可进行微调。



### 肢体障碍 <a href="#entbx" id="entbx"></a>

<mark style="color:blue;">切换控制</mark>

使用各种自适应切换硬件和无线游戏手柄来控制设备。对应iOS的切换控制、Android的开关控制。



<mark style="color:blue;">语音控制</mark>

对应iOS的语音控制和Siri、Android的Voice Access。



<mark style="color:blue;">辅助控制</mark>

iOS的，可以根据自己的肢体活动的需要调节触控屏，切换成自己能用的手势，或者创建专属的触控操作。



### 认知障碍 <a href="#jfyl7" id="jfyl7"></a>

<mark style="color:blue;">引导访问</mark>

iOS的，暂时将设备限制于单个应用，并让你控制哪些功能可用，帮助保持专注。



<mark style="color:blue;">减弱动态效果</mark>

iOS的，用户可能因为动态效果而引起眩晕不适，开启此功能减弱画面的移动效果。



## 04 辅助功能的运行原理 <a href="#gh89k" id="gh89k"></a>

辅助技术根据各自所实现的功能不同，与用户代理、客户端应用、平台级可访问性API直接进行信息的传递和交换。流程图如下图所示：

<figure><img src="../../.gitbook/assets/640 (14).png" alt=""><figcaption></figcaption></figure>

