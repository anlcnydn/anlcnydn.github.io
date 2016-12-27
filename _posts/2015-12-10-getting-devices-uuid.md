---
layout: post
title: Getting The Device's UUID
desc: Basically, this post is about getting the uuid of an Android device.
keywords: "android, uuid, java"
date: 2015-12-10
categories: [Mobile]
tags: [android, uuid, java]
icon: fa-bookmark-o
---
Below code snippet will help you to get the device's uuid..

{% highlight java %}

	TelephonyManager tManager = (TelephonyManager)
						getSystemService(Context.TELEPHONY_SERVICE);
	String uuid = tManager.getDeviceId();
{% endhighlight %}

In order to make this code snippet legal, we need to define
the following xml node in the application manifest:

```
	<uses-permission android:name = "android.permission.READ_PHONE_STATE"/>

```
