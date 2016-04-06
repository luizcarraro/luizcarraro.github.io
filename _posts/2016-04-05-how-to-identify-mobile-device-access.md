---
layout: post
title: How to identify access from mobile devices
tags: [mobile, access, identify, ios, android]
excerpt_separator: <!--more-->
---

If you open a console at your browser and hit ```console.log(navigator)``` you should get a bunch of information about your current session, such as your browser info and OS info. 

That said, all we need to do is parse for some keyword that we'll find at android devices, ios devices, and windows phone devices. The following may serve as example:

{% highlight javascript linenos %}
// Check Android
if (navigator.userAgent.match(/Android/i)) {
    // Do stuff for Android
}

// Check iOS
if (navigator.userAgent.match(/iPhone|iPad|iPod/i)) {
    // Do stuff for iOS
}

// Check windows Phone
if (return navigator.userAgent.match(/IEMobile/i)) {
    // Do stuff for Windows Phone
}
{% endhighlight %}

This worker for me at this date.