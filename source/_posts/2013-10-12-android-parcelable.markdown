---
layout: post
title: "Android 序列化 -- Parcelable"
date: 2013-10-12 12:08
comments: true
categories: android java serialization
---


### 序列化


+ 为什么要序列化？
	1. 永久性保存对象，保存对象的 _字节序列_ 到本地文件中
	2. 通过序列化在网络中传递对象。
	3. 通过序列化在进程间传递对象。				

+ 序列化：
将数据结构或者对象 state 转换成可以存储的格式（如文件，memory buffer，或者在网络上传输），之后再在相同的计算机或者不同的计算机环境中恢复。当生成的bits序列按 _serilization 格式_被重新读出时，它可以创建一个语义唯一（semantically identical） 的原始对象的克隆。 		
序列化的过程也被叫做 deflating 或者 marshalling 。相反的操作则叫做 deserialization （也叫做 inflating 或者 unmarshalling ）。  

+ _序列化格式_:
	* XML , 有常规的xml(human readable text-based encoding,可以用文本编辑器打开) 和 Binary xml。在20世纪，XML经常被用于Ajax网站应用的客户端和服务器之间的数据结构的异步传输。
	+ JSON， 是一个较之于XML 更加轻量级的序列化格式，JSON 也普遍被用于web 应用的C/S通讯， JSON 基于JavaScript 语法格式，不过也支持其他编程语言。
	+ YAML， 高效的JSON超集，包括了一些特性使得它拥有更加强大的序列化功能，对人更加友好，拥有更好的潜在兼容性。
	+ MAC OS X Cocoa..
</br>
</br>
		
+ _编程语言支持_
	+ Java -- java.io.Serializable interface ...
	+ ... 		

参考：wiki百科 [Serilization](http://en.wikipedia.org/wiki/Serialization)


******

</br> 
### 安卓序列化
+ Android 序列化的两种方法
	a. Serializable 接口
	b. [Parcelable](http://developer.android.com/reference/android/os/Parcelable.html) 接口


#### 实现 Parcelable 接口实现安卓序列化		


+ implemnts Parceable 
+ 需要序列化的类必须有一个 static field ： CREATEOR （ CREATEOR 是一个实现了Parcelable.Creator 接口的对象）
 
* 代码示例：
	+ 目的： 实现 Parcelable 接口用于进程间（？）传递对象。程序的运行流程是： 点击MyParcelable 的button ，启动ActivityB 并将一个Person 实例传递过去，然后再再ActivityB 中将收到的Person 对象的信息显示在Textview 上。
	+ 主要结构： 一个Project， 建两个Activity-- MyParcelable，ActivityB 。 MyParcelable 布局中添加一个button， 为Button 添加属性:		
	android:onClick="onClick"		
	ActivityB 的xml 布局里添加一个TextView。		
	一个 Person 类实现 Parcelable 接口。		
	+ 代码： 

MyParcelable :	
		
	public class MyParcelable extends Activity implements OnClickListener {

		@Override
		protected void onCreate(Bundle savedInstanceState) {
			super.onCreate(savedInstanceState);
			setContentView(R.layout.activity_main);
		}

		@Override
		public boolean onCreateOptionsMenu(Menu menu) {
			// Inflate the menu; this adds items to the action bar if it is present.
			getMenuInflater().inflate(R.menu.main, menu);
			return true;
		}

		@Override
		public void onClick(View v) {
			switch (v.getId()) {
			case R.id.btn1:
				Intent intent = new Intent();
				intent.setClass(this, ActivityB.class);
				Bundle extras = new Bundle();
				extras.putParcelable(Person.PARCELABLE_KEY, new Person("Libelosophy", 100));
				intent.putExtras(extras);
				startActivity(intent);
			}
		}
	}

ActivityB :
		
	public class ActivityB extends Activity {
		private TextView tv = null;
	
		@Override
		protected void onCreate(Bundle savedInstanceState) {
			super.onCreate(savedInstanceState);
			setContentView(R.layout.activity_activity_b);
			tv = (TextView) findViewById(R.id.textview);
		
			Person person = getIntent().getExtras().getParcelable(Person.PARCELABLE_KEY);
			String person_info = "Name: " + person.getmName() 
									+ "\n Age: " + person.getmAge();
		
			tv.setText(person_info);
		
			}		
	}


Person :		
		
			
	public class Person  implements Parcelable {
		public static final String PARCELABLE_KEY = "PersonParcelableObject";

		private String mName;
		private int mAge;


		public String getmName() {
			return mName;
		}

		public void setmName(String mName) {
			this.mName = mName;
		}

		public int getmAge() {
			return mAge;
		}

		public void setmAge(int mAge) {
			this.mAge = mAge;
		}

		Person(String name, int age) {
			setmName(name);
			setmAge(age);
		}

	
	
		private Person(Parcel in) {

			setmName(in.readString());
			setmAge(in.readInt());
		}

		@Override
		public int describeContents() {
			return 0;
		}

		@Override
		public void writeToParcel(Parcel dest, int flags) {
			dest.writeString(getmName());
			dest.writeInt(getmAge());
		}

		public static final Parcelable.Creator<Person> CREATOR = new Parcelable.Creator<Person>() {

			@Override
			public Person createFromParcel(Parcel source) {

				return new Person(source);
			}

			@Override
			public Person[] newArray(int size) {

				return new Person[size];
			}
		};

	}

运行结果： 如预期。


* 实例































































