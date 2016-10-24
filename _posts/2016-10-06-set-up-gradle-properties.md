---
layout: post
title:  "Set up Android Studio projects"
date:   2016-10-06 14:00:00 +0300
categories: android
---

My settings for Android Studio projects.

gradle.properties

```groovy
org.gradle.jvmargs=-Xmx2048m -XX:MaxPermSize=512m -XX:+HeapDumpOnOutOfMemoryError -Dfile.encoding=UTF-8
```

build.gradle

```groovy
android {
    dexOptions {
        javaMaxHeapSize "2g"
    }
}
```