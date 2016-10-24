---
published: true
layout: post
title:  "A safe way to manage api keys"
date:   2016-10-22 12:00:00 +0300
categories: android, gradle, java, xml, git, api
---

Some times ago i faced with the problem - "Where to store api keys and don't commit them to the public git repository one day?". I made research and found next solutions:

## 1. Store api keys in a xml file
Put xml file "api_keys.xml" in the directory "res/value/".

*api_keys.xml*
```xml
<?xml version="1.0" encoding="utf-8"?>
<resources>
    <string name="THE_MOVIE_DB_API_TOKEN">XXXXX</string>
</resources>
```

*use api keys in java code*
```java
getString(R.string.THE_MOVIE_DB_API_TOKEN);
```

---

## 2.1 Store api keys with help of gradle and the gradle.properties file (Java)

[Example_0](https://github.com/udacity/Sunshine-Version-2/commit/898f4355c4bb257055f9f0eb2ac51e0412674cbf)
[Example_1](https://github.com/udacity/Sunshine-Version-2/blob/sunshine_master/README.md)
[Example_2](http://michiganlabs.com/string-constants-generated-gradle-build-configurations/#.VtB0-px96Um)

Add the following line to [USER_HOME]/.gradle/gradle.properties

*For Windows OS, example for Denis user:* 
```
C:\Users\Denis\.gradle
```

*gradle.properties*
```xml
MyTheMovieDBApiToken="XXXXX"
```

Add the following code to the build.gradle file

*build.gradle*
```gradle
apply plugin: 'com.android.application'

android {
    ...

    defaultConfig {
        ...
    }
    buildTypes {
        release {
            ...
        }
        buildTypes.each {
            it.buildConfigField 'String', 'THE_MOVIE_DB_API_TOKEN', MyTheMovieDBApiToken
        }
    }
}
```

*use api keys in java code*
```java
BuildConfig.THE_MOVIE_DB_API_TOKEN)
```

## 2.2 Store api keys with help of gradle and the gradle.properties file (Java + XML)

*gradle.properties*
```
AppKey="XXXX-XXXX"
```

*build.gradle*
```groovy
buildTypes {
//...
    buildTypes.each {
        it.buildConfigField 'String', 'APP_KEY_1', AppKey
        it.resValue 'string', 'APP_KEY_2', AppKey
    }
}
```

*Usage in java code*
```java
Log.d("UserActivity", "onCreate, APP_KEY: " + getString(R.string.APP_KEY_2));

BuildConfig.APP_KEY_1
```

*Usage in xml code*
```xml
<data android:scheme="@string/APP_KEY_2" />
```

---

## 3. Store api keys with help of gradle and the system path variable

[Example_0](http://stackoverflow.com/questions/9854176/in-gradle-is-there-a-better-way-to-get-environment-variables)

Add new system PATH variable *THE_MOVIE_DB_API_TOKEN="XXXXX"*:
### For Windows OS:
* open system
* advanced system settings
* environment variables
* add new variables to the user variables 


Add the following code to the build.gradle file

*build.gradle*
```gradle
apply plugin: 'com.android.application'

android {
    ...

    defaultConfig {
        ...
    }
    buildTypes {
        release {
            ...
        }
        buildTypes.each {
            it.buildConfigField 'String', 'THE_MOVIE_DB_API_TOKEN', "$System.env.THE_MOVIE_DB_API_TOKEN"
        }
    }
}
```

*use api keys in java code*
```java
BuildConfig.THE_MOVIE_DB_API_TOKEN)
```

### Link to my gist on GitHub

[My store api keys gist](https://gist.github.com/VDenis/46c222b16683447bab33)

### Answers on the same topic on Stack Overflow:

* [Is it possible to declare a variable in Gradle usable in Java?](http://stackoverflow.com/questions/17197636/is-it-possible-to-declare-a-variable-in-gradle-usable-in-java/35650390#35650390)
* [Is there a safe way to manage API keys?](http://stackoverflow.com/questions/33134031/is-there-a-safe-way-to-manage-api-keys/34021467#34021467)
