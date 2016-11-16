# Overview
![Wit SDK for Ionic Framework](http://witsdk.com/images/wit-banner-beta.png)
Welcome! WIT is a powerful mobile SDK that helps you build mobile apps which work offline and in real time.
The SDK will always use the best technology to deliver your mission critical data.

### Download
Download the latest official release of Wit SDK and get started!
[[Download v0.1.13 "Big Bang"]()](https://witsdk.com/releases/ionic/witsdk_0.1.13-big-bang.zip)

Latest Version: 0.3 "Big Bang"
Released: 2016-11-16

### What can do WIT for me?

It gives you the unique value to be there for your customers anytime, even when they are offline.
You can make your service available for emerging markets, traveler abroad and anybody who have a smartphone which is not connected to the Internet.

### Things to keep in mind:

* WIT-SDK works on Android < 6, support for Android 6 will come soon.
* This SDK is built for [Ionic Framework 1.x](http://ionicframework.com/docs/overview/#download) + [ngCordova](http://ngcordova.com/docs/install/) (Ionic2 when the stable version is out).
* This is a closed beta meaning something might not work sometime.
* Your feedback is the most important thing at this stage.

# Installation

### Platform notes
First, we need to start with a note about minimum requirements for building your app with the current release of Wit SDK. Wit SDK targets Android devices (currently). We support Android < 6. However, since there are a lot of different Android devices, it’s possible certain ones might not work. As always, we are looking for help testing and improving our device compatibility and would love help from the community in identifying bugs.

### Get the bundle file
Download the zip file here, and locate the .js file in the dist folder:

Include ```wit.bundle.min.js``` in your index.html file  after your AngularJS / Ionic file (since Wit SDK depends on AngularJS).


```html
<script src="lib/ionic/js/ionic.bundle.js"></script>
<script src="wit-sdk/dist/wit.bundle.min.js"></script>
```

### Inject as an Angular dependency

Then, include Wit SDK as a dependency in your angular module:

```javascript
angular.module('myApp', ['ngCordova', 'witSdk'])
```

### Wrap ```$wit.init()``` call with the ```deviceready``` event - important !

Before using Wit you must check if your device has fully loaded, and if the plugins are available using a native cordova event called deviceready. Implement it like so:

```javascript
ionic.Platform.ready(function(){
      $wit.init();
});
```

### Add the plugins to your project using the Cordova CLI

```
cordova plugin add cordova-plugin-sms
cordova plugin add cordova-plugin-device
cordova plugin add cordova-plugin-network-information
```

# $wit service

```$wit``` is the service which will replace ```$http``` to make your http calls support offline mode.

```$wit``` works similarly to ```$http``` Angular Service does, good news is you already know how to use it!

Here an example of a regular http post request:

```
$http.post('http://myawesomeservice/api/v1/goodstuff, payload)
.then(function(data){
  console.log("I do things with the data", data);                      
});
```

Let’s now see how a **WIT post **request looks like:

```

$wit.request({
	"url": "your.endopoint.url",
	"type": "POST||GET||PATCH||PUT||DELETE",
	"secure": "true||false" // https? default is false 
}, 
payload)
.then(function(data){
  console.log("I do things with the data", data);                      
});
```

Yep, it's that easy. WIT will return a promise with the data you normally get back from an http call.

### Support
This version of the SDK supports Ionic 1.x on Android < 6. It will work on real android device, the android emulator and the browser will not work because the client needs to be able to receive SMS.

### Licence
Copyright (C) WIT Technology, LTD - All Rights Reserved
