---
description: >-
  TotalCross is a cross-platform tool that lets you develop apps in JAVA and
  deploy them to iOS, Android and Windows easily, leading to 3x cost and time
  savings.
---

# TotalCross Overview

Our vision is **to create the next generation of cross-platform tools** and help Java developers and companies to **easily create beautiful mobile applications** for all platforms on the market.

* Track all TotalCross updates through the [customer space.](http://www.superwaba.net/SDKRegistrationService/)
* Ask for feature request or vote for existing ones on GitLab [The TotalCross Companion](https://gitlab.com/totalcross/TotalCross/issues) remember to tag it with `feature`
* Found a bug? Please open an [issue](https://gitlab.com/totalcross/TotalCross/issues)
* Follow the [blog ](https://blog.totalcross.com/)posts to access marketing, development, technology and more

## Supported Platforms

* **Android** 4.0.3 and above \(API level 15\)
* **iOS** 8.0 and above.
* **Hand Held** \(Honeywell, Zebra, etc\).
* **Windows** XP and above.
* **Linux** 32 bits \(Debian distribution only\).
* **Java** applet \(JDK 1.1 and above\)
* **Raspiberry PI**
* **Toradex** 

{% hint style="success" %}
The choice of Java as a language for development was not occasional, but due to the fact that of the **21 million existing developers** in the world, **9 million are Java developers**, according to the Global Developers Population and Demographic Study in 2016.   
**It is one of the largest development communities in the world!**
{% endhint %}

## Virtual Machine Features

In our heart is present our virtual machine, originally idealized in a master's degree, and already built and perfected over 10 years. It's log-based \(Java\) architecture, bytecode _"itself with its own folders"_ for the most frequent and **implemented 100% with C guarantees performance equivalent to native development.**

This is how TotalCross applications can run not only on Android or iOS devices but also on desktops and hand helds \(Honeywell, Zebra, etc.\) or kiosks that can do Android, Windows or WinCE, supporting devices with the processor of 500Mhz and only 64MB of RAM.

### TotalCross Virtual Machine features

#### The TotalCross Virtual Machine \(TCVM\) is a shared library written from scratch, and has the following features:

* It interprets a proprietary set of opcodes instead of Java Bytecodes. 
* It is a register-based VM, not stack-based as Java, which results in **better performance.** 
* **It has support for real multi-threading**. Note that the TotalCross API does not supports concurrency, which must be implemented by your own. 
* The TotalCross class \(tclass\) files stores internal information in little endian, since its the most widely used format of actual microprocessors. 
* **The tclass files are highly optimized to save space**. For instance, the constant pool \(where strings, constants, and identifiers are stored\) is shared among all deployed classes, and each class entry is compressed using zlib. 
* **Supports headless applications** \(like daemon applications, without user interface\): just implement the interface totalcross.MainClass and this class will be loaded by the TCVM. The appStarting\(\) and appEnding\(\) methods are called and the application exits. 
* **Supports the method finalize\(\)**, ran every time the garbage collector \(gc\) finishes its job. There’s a limitation: no objects can be created inside a finally method, otherwise the method will silently abort itself. Optionally, to improve GC’s performance, you can define in your class a public non-static field named dontFinalize that, if present and set to true, will skip the finalize call. In most cases, finalize\(\) is used to ensure that a class that holds system resources \(like file or socket\) and should be closed to release these resources is always closed, either because the programmer forgot to do it himself or because the program was halted by an exception. Note that you must define the field dontFinalize and set it to true when the close method is run for the first time. Otherwise the gc will try to finalize an object that was already closed by the programmer, which may cause trouble. Doing so also speeds up the gc. 

### The TotalCross VM also has a drawback:

It does not support the float type, only double. This option was adopted because all actual processors have a math co-processor, and also because the vast majority of mobile applications are not scientific programs. During our research, we found that float types are two times faster than double, but this small performance difference does not make up for the overhead needed to add float type support to the virtual machine. The change from float to double will be done by the translator to let legacy applications work, however, you should change your application to use double, since there’s no benefit by using float.

## Thread Support

TotalCross supports preemptive threads using the native thread mechanism of each supported platform. On Android, iOS, and Linux, it uses pthread, and on Windows, it uses the qte well documented thread api.

The API does not support concurrency. If your program needs to access the same object from many threads, you must use the synchronized keyword. The support for synchronized is limited: it does not support synchronized methods, neither classes, neither standard objects. You must use the synchronized\(object\), and the only object type that can be used as parameter is the totalcross.util.concurrent.Lock. If you use synchronized\(this\), the tc.Deploy will abort during deploy; if you use synchronized with an object from any other class besides the Lock class, a RuntimeException will be thrown when your program runs in the TotalCross virtual machine. Moreover, using the synchronized keyword before a method will be useless: it will be ignored by the VM. Note that these problems will not occur when running on Java desktop, only when running on TCVM. Here’s a sample that shows how to use it:

```java
\lstinputlisting[label=samplecode,caption=A sample]companion_resources/listings/TestConcurrent.java
```

In the sample above, commenting out the line marked with \*\*\*\*\*, the log list box will be filled randomly by the threads. With the lock, it will be filled in sequence, because each thread will gain the lock once, and the other threads will have to wait the main loop of the lock owner finish before starting their loops. There’s no limit in the number of locks used.

Generally speaking, you can create a thread to listen to a socket or a file or even a Litebase table in background, but be aware that if you try to access the same resource by different threads your application might just blow up. We also don’t recommend running the user interface in a background thread, due to system event concurrency. Threads should be used for I/O and other tasks, but not for showing user interface screens that could receive events.  


## Graphics, Palette and Color

TotalCross has a graphics engine written from scratch, and some important performance-tailored decisions were taken.

Regardless of the device’s color depth, the screen and images are stored in a 24 bpp RGB array. All drawings are made into a single off screen, which is then converted on the fly to the device’s screen color depth when the updateScreen\(\) method is called. Note that since 2011, no devices with 8 bpp are released to the market; all of them use at least 16 bpp \(65536 colors\).

The Graphics class **supports real clipping**, which allowed us to support containers that automatically show scrollbars if components are placed beyond its limits.

**TotalCross also supports screen rotation and collapsible input area**. If the user interface is implemented using only relative coordinates, **it will automatically reposition itself whenever the screen resolution is changed**.

Note that aControl.setRect\(getClientRect\(\)\) should never be used, otherwise the automatic repositioning will not work. Instead, aControl.setRect\(LEFT, TOP, FILL, FILL\) should be used to produce the same result without affecting the repositioning. If you really have to use getClientRect\(\), you must also override the reposition\(\) method to support screen rotation. \(see the WorldWatch sample\).

Colors are represented by int values in the **0xRRGGBB** format. A null color is represented by the value -1.

## Images

Images in TotalCross supports transparency \(also known as alpha-channel\). The best way to show images is to generate a PNG image from a vectorized image through Photoshop or any other good editor. Prefer creating a big image \(for example, 96x96\), then decrease its size at runtime using Image.getSmoothScaledInstance.

## Inheritance and Delegation event models

TotalCross supports both Inheritance \(Java 1.0\) and Delegation \(Java 1.1\) event models. The Inheritance model will make your code smaller and faster, but there are some situations that require the usage of the Delegation model.

### onEvent

```java
public class MyProgram extends Container{
	Button pushB;
	​
	public void initUI(){
		add(pushB = new Button("Push me, please"), CENTER, TOP);
	}
	​
	public void onEvent(Event event){
		switch (event.type){
			case ControlEvent.PRESSED:
			if (event.target == pushB)
			// handle pushB being pressed
			break;
		}
	}
}

```

### Listener

```java
public class MyProgram extends Container{
	Button pushB;
	​
	public void initUI(){
		add(pushB = new Button("Push me\nPlease"), CENTER, TOP);
		pushB.addPressListener((e) -> {
			// handle pushB being pressed
		});
	}
}

```

## Security

TotalCross applications are currently impossible to be decompiled, because, as mentioned before, TotalCross uses a proprietary set of opcodes instead of Java Bytecodes. The translation between Java Bytecodes to TotalCross opcodes is done automatically when the application is deployed.

However, this also means that you cannot retrieve your application’s source files from the deployed application, so don’t forget to backup your source files!

