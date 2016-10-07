# A simple test application to integrate Scala and a Windows DLL

This code was created in order to allow the integration of Scala and a Windows DLL. It was entirely based in [this example](http://hohonuuli.blogspot.com.br/2013/08/a-simple-java-native-interface-jni.html), so I just had to create the DLL and manage to integrate both platforms.

If your are used to JNI, you'll see that there is no much difference between Java and Scala, except that in the last you have to include Scala Library and Scala Reflect libraries in the source path (sure, there are few differences in coding).

In order to make it work in Linux or Unix, just follow those steps in the link above: it works like a charm.


# Steps to make the whole thing work

In __Sample1Scala__ folder, run the following commands:

```
scalac Sample1.scala
set SCALA_CP=%SCALA_LIB%\scala-library.jar;%SCALA_LIB%\scala-reflect.jar
javah -classpath %SCALA_CP%;.\ Sample1
```
* Sure, you must have Scala installed in your computer and __SCALA_LIB__ variable configured to reflect its lib folder (search for those __scala-library.jar__ and __scala-reflect.jar__ files if you are not sure where they are);
* This will create the __Sample.h__ file that is used in __Sample1DLL__ project (created just as a reference in this last step). The __Sample1.cpp__ file was created with the source code provided in the example referenced previously.

Then, compile the DLL and copy it to __Sample1Scala__ folder;
Lastly, run the following command to call Sample1 application.

```
java -cp %SCALA_CP%;. Sample1
```

# Important notice

Make sure you use the same target platform for your DLL that corresponds to the installed JVM (run __java -version__ to check). If your JVM is a 64 bit version, compile to a x64 DLL, otherwise, compile it to a x86 DLL. These options can be configured in Visual Studio.
