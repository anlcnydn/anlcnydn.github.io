---
layout: post
title: Calling startActivity() From Outside of an Activity Context
desc: Aim of this post is to describe and exemplify calling startActivity() method from outside of an activity context.
keywords: "android,broadcast-receiver,intent,startActivity"
date: 2015-11-29
categories: [Mobile]
tags: [android, broadcast-receiver, intent]
icon: fa-bookmark-o
---

[Broadcast Receivers](http://www.tutorialspoint.com/android/android_broadcast_receivers.htm) simply respond to broadcast messages from other applications or from the system itself. These messages are sometimes called events or intents. For example, applications can also initiate broadcasts to let other applications know that some data has been downloaded to the device and is available for them to use, so this is broadcast receiver who will intercept this communication and will initiate appropriate action.

Appropriate action can change from one situation to another by programmer's decision. Sometimes a [Toast](http://developer.android.com/intl/es/guide/topics/ui/notifiers/toasts.html) will be popped up, sometimes another broadcast and sometimes another **Activity** will be started.

For example:

{% highlight java %}
public class CustomReceiver extends BroadcastReceiver {

    @Override
    public void onReceive(Context context,
                            Intent intent) {
    	String response = intent.getStringExtra();

    	if(!response.isEmpty()){
    		Intent i = new Intent(context,
                        SomeOtherActivity.class);

            i.putExtra("RESPONSE_EXTRA",repsonse);
    		startActivity(i);
    	}
        else{/*Implemented code here*/}

	}
}
{% endhighlight %}

This code snippet will probably get error like:

> Calling startActivity() from outside of an Activity  context requires the FLAG_ACTIVITY_NEW_TASK flag. Is this really what you want?

Because of the context can come from anywhere. In order to make this code snippet functional, it should be changed in a way that:

{% highlight java %}
public class CustomReceiver extends BroadcastReceiver {

    @Override
    public void onReceive(Context context,
                            Intent intent) {
    	String response = intent.getStringExtra();

    	if(!response.isEmpty()){
    		Intent i = new Intent(context,
                        SomeOtherActivity.class);

            i.putExtra("RESPONSE_EXTRA",repsonse);
    		i.setFlags(Intent.
                FLAG_ACTIVITY_NEW_TASK);
    		startActivity(i);
    	}
        else{/*Implemented code here*/}

	}
}
{% endhighlight %}

This will work.
