# Zip Manager ANE V2.9.2 (Android+iOS)
ZipManager class will zip or unzip large zip archives super fast using native process in threads supporting both Android and iOS. you will have listeners to watch the process progress. you have the option to cancel a zip or unzip progress. it's job is to concentrate on zip archiving and it does it in the best possible way!

in AS3, there are many different zip libraries which will do the same thing but they are not good enough when it comes to mobile usage because of the following reasons:

� They load the whole zip into runtime and then try to zip/unzip reading bytes which is too time consuming
� loading a big zip file using AS3 libraries will fail on mobile devices because it takes too much RAM
� AS workers are not yet supported on iOS and your Air UI will freez untill the process is finished!
� the bottom line is that AS3 libs for handling zip files are TOO slow and not practical

using this extension will solve all the above problems. you will be amazed how fast it works no matter the size of the zip file. we tested with a ~1GB zip archive and it worked just fine :) 

checkout here for the commercial version: http://www.myflashlabs.com/product/zip-ane-adobe-air-native-extension/

![Zip Manager ANE](http://www.myflashlabs.com/wp-content/uploads/2015/11/product_adobe-air-ane-extension-zip-manager-595x738.jpg)

you may like to see the ANE in action? check this out: https://github.com/myflashlab/zipManager-ANE/tree/master/FD/dist

**NOTICE: the demo ANE works only after you hit the "OK" button in the dialog which opens. in your tests make sure that you are NOT calling other ANE methods prior to hitting the "OK" button.**

# AS3 API:
```actionscript
import com.myflashlab.air.extensions.zip.ZipManager;
import com.myflashlab.air.extensions.zip.ZipManagerEvent;

var _ex:ZipManager = new ZipManager();
_ex.addEventListener(ZipManagerEvent.START, onStart);
_ex.addEventListener(ZipManagerEvent.ERROR, onError);
_ex.addEventListener(ZipManagerEvent.PROGRESS, onProgress);
_ex.addEventListener(ZipManagerEvent.COMPLETED, onComplete);

_ex.unzip(File.documentsDirectory.resolvePath("TheZipFile.zip"), File.documentsDirectory.resolvePath("unzipLocation"));

function onStart(e:ZipManagerEvent):void
{
   trace("zip process started...");
}

function onError(e:ZipManagerEvent):void
{
   trace("zip process ERROR: " + e.param.msg);
}

function onProgress(e:ZipManagerEvent):void
{
   trace("zip Progress = " + e.param.perc + "%");
}

function onComplete(e:ZipManagerEvent):void
{
   trace("[zip process finished]");
}
```

on the Android side, you need the following permission because your zip content must be on File.documentsDirectory

```xml
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"/>
```

# Changelog
* Jul 06, 2013	>> V1.0, 	beginning of the journey!

* Nov 07, 2014	>> V2.0, 	rebuilt the whole thing to add support for iOS
  *		>> V2.0, 	supports Android-ARM, Android-x86, iPhone-ARM
  *		>> V2.0, 	processes the zip works on threads natively both on Android and iOS
  *		>> V2.0, 	depricated the download zip methods. we have a separated powerful DownloadManager class for this job: http://myappsnippet.com/download-manager-air-native-extension/
  *		>> V2.0, 	added methods to cancel zipping or unzipping progresses

* Jan 27, 2015	>> V2.1, 	added support for iOS 64-bit

* May 16, 2015	>> V2.2, 	removed android-support-v4 dependency

* Nov 03, 2015	>> V2.9,	doitflash devs merged into MyFLashLab Team.
* Dec 20, 2015 	>> V2.9.1: 	minor bug fixes

* Jan 20, 2016 	>> V2.9.2: 	bypassing xCode 7.2 bug causing iOS conflict when compiling with AirSDK 20 without waiting on Adobe or Apple to fix the problem.
  *							This is a must have upgrade for your app to make sure you can compile multiple ANEs in your project with AirSDK 20 or greater.
  *							https://forums.adobe.com/thread/2055508
  *							https://forums.adobe.com/message/8294948