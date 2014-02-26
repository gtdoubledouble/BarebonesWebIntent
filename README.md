BarebonesWebIntent
==================

Cordova + WebIntent

Basically, this is to show the minimum needed to get a Cordova mobile application to process incoming URL as intents, at least on the Android-side.
In other words, when you click on a certain link in your browser, you can choose to use this app to open it (thus doing whatever you want with it).

While you can clone this project to see how it works, what I did was:
Install Cordova and create a project.
Get the [WebIntent plugin](https://github.com/Initsogar/cordova-webintent) and follow the instructions.
Add Android platform with Cordova, build it.
Make sure res/xml/config.xml contains the line:
> <plugin name="WebIntent" value="com.borismus.webintent.WebIntent" />

In index.js, append this piece of code:

> window.plugins.webintent.getUri(function(url){
            if(url !== ""){
                console.log('hey I got something1');
                console.log('URL was + ' + url);
                $('#test').innerHTML = "URL was" + url;
            }
            console.log('hey I got something2');
        });

In AndroidManifest.xml, append this piece of code:
            <intent-filter>
                <action android:name="android.intent.action.VIEW" />
                <category android:name="android.intent.category.DEFAULT" />
                <category android:name="android.intent.category.BROWSABLE" />
                <data android:host="www.youtube.com" android:scheme="http" />
                <data android:host="checklist" android:scheme="http" />
            </intent-filter>
  
Replace the last two with anything you want - if you want myapp://, then you should change android:scheme="http" to "myapp"

Tap on some link in your Android browser, and this app should open
