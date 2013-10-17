---




---



## android 基础复习

### Application Fundamentals

android 程序用java 语言写成，经 ADT 编译后同其他数据和资源文件一起打包成 apk，一个apk 被认为是一个应用程序。基于 android 的设备用这个apk 来安装应用程序（application）。

Once installed on a devices, each Android application lives in its own security sandbox: 
	+ The Android system is a multi-user Linux system in which each application is a different user.
	+ By default, the _system_ assigns each application a unique Linux  user ID ( the ID is used only by the _system_ and is unknown to the application). The _system_ sets permissions for all the files in an application so that only the user ID assigned to that application can accsess them.
	+ Each precess has its own virtual machine (VM), so an application's code runs in isolation from other applications.
	+ By default, every application runs in its own Linux process.Android starts the process when any of the application's compnents need to be executed, then shuts down the process when it's no longer needed or when the system must recover memory for other applications.

每个应用程序都是一个用户？ 本来我以为每个程序的所有者都会不一样，结果
在adb shell 里查看 /system/app/ 里的文件信息，如下： 

	-rw-r--r-- root     root       395261 2013-09-22 00:44 AirkanPhoneService.apk
	-rw-r--r-- root     root        98414 2013-10-12 00:04 AntiSpam.apk
	......
	
system/app 里的所有应用的所有者和组都是 root 
然后查看 /data/app/ 里的apk文件信息， 如下： 

	-rw-r--r-- system   system     361893 2013-08-17 18:28 AlipayMsp.apk
	-rw-r--r-- system   system    4042163 2013-10-12 00:22 MiuiVideo.apk
	-rw-r--r-- system   system   10945819 2013-09-14 10:49 VoiceAssist.apk
	-rw-r--r-- system   system    4404684 2013-10-06 17:06 cn.amazon.mShop.android-1.apk
	-rw-r--r-- system   system    5006289 2013-09-17 16:53 cn.kuaipan.android-2.apk
	......

所有 apk 的所有者和组都是 system ， 想到 Linux 里面在文件里面有存储 用户信息 ，于是找到了 data/user/0/

	shell@android:/data/user/0 # ls -l
	
	drwxr-x--x u0_a132  u0_a132           2013-10-06 17:07 cn.amazon.mShop.android
	drwxr-x--x u0_a57   u0_a57            2013-08-17 19:16 cn.kuaipan.android
	drwxr-x--x u0_a84   u0_a84            2013-10-06 16:44 com.UCMobile
	drwxr-x--x u0_a73   u0_a73            2013-08-25 11:58 com.adobe.flashplayer
	drwxr-x--x u0_a105  u0_a105           2013-08-23 19:35 com.aibang.abbus.bus
	drwxr-x--x u0_a95   u0_a95            2013-09-12 06:57 com.aide.ui
	drwxr-x--x u0_a125  u0_a125           2013-10-07 00:12 com.alibaba.mobileim
	drwxr-x--x u0_a49   u0_a49            2013-08-25 11:58 com.alipay.android.app
	......

可以看见有系列对应与 apk 的文件夹， 而每个文件夹的所有者几乎都不相同（官方文档里说不同的应用程序也可以有相同的用户ID）。但是，_为什么在.apk 那里的所有者全都是 system ，而给了/data/user/0/ 里对应的文件夹不同的所有者？_		
插入一点东西
>1. 应用程序的可执行文件是什么？
就是说类似与windows 上的 .exe ，java 的 字节码， 解压.apk,可以得到一个 .dex 文件， dex 是Dalvik Executable Format 的缩写，即dalvik 可执行格式， 我知道java 用java 虚拟机，而android 用的是 Dalvik 虚拟机。、
PS: 谷歌对 Dalvik 虚拟机及 DEX 的解释在： [Dalvik](http://source.android.com/devices/tech/dalvik/)  。 		
>2. Dalvik 如何执行应用程序？
 执行 dex 文件里的指令？ 

目前我作如此假设， system 是.apk 文件的所有者， 于是它可以对apk 进行操作（比如说，载入内存中执行？？？），system 对每个应用程序都分配一个ID来设置权限，就如同文档说的为每个应用里的文件设置权限。而每个应用都有自己VM ，那么对于程序自己来说就没有什么用户的概念了。



In this way, the Android system implements the _principle of least privilege_ . That is , each application, by default,has a access only to the components that requires to do its work and no more. This creats a very secure environment in which an application cannot access parts of the system for which it is not given permission. 

However, there are ways for an application to share data with other applications and for an application to access system servicesa:

+ It's possible to arrange for two application to share the same Linux user ID , in which case they are able to access each other's files. To conserve system resources, applications with the same user ID can also arrange to run in the same Linux process and share the same VM(the applications must also be signed with the same certificate).
+ An application can request permission to access device data such as user's contacts, SMS messages, the mountable storage(SD card) , camera, Bluetooth, and more . All application permissions must be granted by the user at install time.
That covers the basics regarding how an Android application exists within the system. 




### Activities

#### Activity 的生命周期
onCreate   
onStart  
onResume  onRestart     
onPause  
onStop  
onDestory  

	public class ExampleActivity extends Activity {
	    @Override
	    public void onCreate(Bundle savedInstanceState) {
		super.onCreate(savedInstanceState);
		// The activity is being created. 
		// Your activity should perform setup of "global" state (such as defining layout) in onCreate()
	    }
	    @Override
	    protected void onStart() {
		super.onStart();
		// The activity is about to become visible.
	    }
		
		// onResume and onPause 
		//Because this state can transition often, the code in these two methods should be fairly lightweight in order to avoid slow transitions that make the user wait.
	    @Override
	    protected void onResume() {
		super.onResume();
		// The activity has become visible (it is now "resumed").
	    }
	    @Override
	    protected void onPause() {
		super.onPause();
		// Another activity is taking focus (this activity is about to be "paused").
	    }
	    @Override
	    protected void onStop() {
		super.onStop();
		// The activity is no longer visible (it is now "stopped")
	    }
	    @Override
	    protected void onDestroy() {
		super.onDestroy();
		// The activity is about to be destroyed.
		// release all remaining resources in onDestroy()
	    }
	}


#### 保存 Activity state

当Activity 处于 paused 或stopped 状态时，Activity的state 仍然是存在的，因为state仍然在内存中，所有的成员和当前states都存在与内存，因此当 activity resume时，这些改变都会保持。  
然而，如果系统为了回收内存而销毁了activity 对象，系统就不能简单的从保留的ｓｔａｔｅ中恢复ａｃｔｉｖｉｔｙ，此时，如果用户回到这个ａｃｔｉｖｉｔｙ，系统必须重新创建activity 对象，










	 
