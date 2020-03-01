# Fragula
A simple and customizable Android fragments navigator with support "swipe to dismiss" gestures and saving a stack of fragments when changing the screen orientation

![](20200301_131107.gif)

### Requirements
* A project configured with the AndroidX
* SDK 21 and and higher

### Demo Application
[![Get it on Google Play](https://play.google.com/intl/en_us/badges/images/badge_new.png)](https://play.google.com/store/apps/details?id=info.yamm.project2&hl=ru)

(The app requires vk.com registration)

### Install
Download via **Gradle**:

Add this to the **project `build.gradle`** file:
```gradle
allprojects {
    repositories {
        ...
        maven { url "https://jitpack.io" }
    }
}
```

And then add the dependency to the **module `build.gradle`** file:
```gradle
implementation 'com.github.shikleyev:fragula:1.0'
```

### Usage
#### Simple usage
All you need to do is create a Navigator in the xml of your activity:
```xml
<?xml version="1.0" encoding="utf-8"?>
<com.fragulo.navigator.Navigator
    android:id="@+id/navigator"
    xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".MainActivity"/>
```

And init Navigator in your activity:
```kotlin
override fun onCreate(savedInstanceState: Bundle?) {
    super.onCreate(savedInstanceState)
    setContentView(R.layout.activity_main)
    navigator.init(supportFragmentManager)
    if (savedInstanceState == null) {
        navigator.addFragment(BlankFragment())
    }
}
override fun onDestroy() {
    navigator.release()
    super.onDestroy()
}
```

#### Passing arguments to a fragment
You can pass an unlimited number of arguments in the function parameters:
```kotlin
navigator.addFragment(
    BlankFragment(),
    Arg(ARG_PARAM1, "Add fragment arg"),
    Arg(ARG_PARAM2, "New arg"))
```
And get them in an opened fragment:
```kotlin
class BlankFragment : Fragment() {

    private var param1: String? = null
    private var param2: String? = null

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        arguments?.let {
            param1 = it.getString(ARG_PARAM1)
            param2 = it.getString(ARG_PARAM2)
        }
    }
}
```

![](20200301_131439.gif)
![](20200301_133838.gif)
![](20200301_133937.gif)
