![Wit SDK for Ionic Framework](http://witsdk.com/images/wit-banner-beta.png)

Welcome! WIT is a powerful mobile SDK that helps you build mobile apps which work offline and in real time.
The SDK will always use the best technology to deliver your mission critical data.

### Download
Download the latest official release of Wit SDK and get started!
[[Download v0.3 "Big Bang"](http://www.witsdk.com/release/wit.bundle.min.js)](https://witsdk.com/release/wit.bundle.min.js)

Latest Version: 0.3 "Big Bang"
Released: 2016-11-16

### What can WIT do for me?

It gives you the unique value to stay connected to your customers anytime, anywhere even when they are offline. You can make your service available for emerging markets, travellers abroad and anyone who has a smartphone not connected to the Internet.

### How does it work?

WIT uses SMS to proxy APIs calls to your backend, the data is received through a promise like regular http requests.

### How should I use WIT?

We suggest you proxy **ONLY light APIs requests** as the latency receiving the data is proportionally related to the amount of data making up the request. This service is meant to be used for **mission critical data**.

We can help in optimizing your request to be faster and use less SMS (up to 70%), [[contact us](alessio@witsdk.com)]() for more informations.

#### Good examples are:

* Taxi hailing apps
* Emergency apps
* Logistic apps to monitor GPS position
* Booking Systems inside apps
* Mobile wallets
* Delivery apps
* IoT management apps
* Stock Options apps
* Weather apps
* Heartquake monitoring apps
* You name it...

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
<script src="wit.bundle.min.js"></script>
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

```$wit``` works very similarly to the way ```$http``` Angular Service does so the good news is you already know how to use it!

Here an example of a regular http post request:

```
$http.post('http://myawesomeservice/api/v1/goodstuff, payload)
.then(function(data){
  console.log("I do things with the data", data);                      
});
```

Let’s now see the equivalent request using WIT:

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

## Examples

### PATCH Request
```
$wit.request({
    type:'patch',
    url:'jsonplaceholder.typicode.com/posts/1'
  },{
    title: 'alto',
    body: 'barrio'
  }).then(function(res){
    console.log('Generic PATCH request response: ',res);
  });
```

### GET Request
```
  $wit.request({
    type:'get',
    url:'jsonplaceholder.typicode.com/posts/12'
  }).then(function(res){
    console.log('Generic GET request response: ',res);
  });
```

### DELETE Request
```
  $wit.request({
    type:'delete',
    url:'jsonplaceholder.typicode.com/posts/1'
  }).then(function(res){
    console.log('Generic DELETE request response: ',res);
  });
```

### POST Request
```
  $wit.request({
    type:'post',
    url:'jsonplaceholder.typicode.com/posts'
  },{
    title: 'foo',
    body: 'bar',
    userId: 1
  }).then(function(res){
    console.log('Generic POST request response: ',res);
  });
```

### PUT Request
```
  $wit.request({
    type:'put',
    url:'jsonplaceholder.typicode.com/posts/1'
  },{
    id: 1,
    title: 'foo',
    body: 'bar',
    userId: 1
  }).then(function(res){
    console.log('Generic PUT request response: ',res);
  });
```

### Support
This version of the SDK supports Ionic 1.x on Android < 6. It will work on real android device, the android emulator and the browser will not work because the client needs to be able to receive SMS.

### License
Copyright (C) WIT Technology, LTD - All Rights Reserved
