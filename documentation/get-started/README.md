---
description: Learn how to install TotalCross and write your first App.
---

# Getting Started

## Host prerequisites

To start using TotalCross, you will need to install this dependencies on your machine:

* VSCode: [Java 11 ](https://www.oracle.com/java/technologies/javase-jdk11-downloads.html)or greater to be compatible with [Language Support for Java\(TM\) by Red Hat](https://marketplace.visualstudio.com/items?itemName=redhat.java);
* Others IDEs: you can use any version since [Java 8](https://learn.totalcross.com/documentation/miscelaneous/java-8);
* [Maven](../miscelaneous/maven.md).

In the next steps you will learn how to quickly setup TotalCross at your favorite IDE. If you have already installed the prerequisites, let's get started!  

{% hint style="warning" %}
On versions 2.0.0 or above from totalcross-maven-plugin you need to agree to the [Terms of Use](https://www.azul.com/products/zulu-and-zulu-enterprise/zulu-terms-of-use/) from Azul, if you don't you can change the jdk used to any Java version you want to use, this is described [here](https://github.com/TotalCross/totalcross-maven-plugin/releases/tag/v2.0.0).
{% endhint %}

## Target Linux Dependencies

TotalCross depends exclusively on 3 things on the **Linux ARM platform**:

1. A graphics server \(eg X11 or Wayland\); 
2. `libfontconfig1-dev`; 
3. `libSDL2-dev`. 

{% hint style="warning" %}
If you intend to run your application on an [Angstrom distribution](http://www.angstrom-distribution.org/), you must follow the steps bellow:

1. Download the[ SDL.zip](https://totalcross-release.s3-us-west-2.amazonaws.com/libs/SDL.zip) compiled to works on Angstrom;
2. Extract the content to `/usr/local/lib/` in your device:

   `mkdir -p /usr/local/lib && unzip SDL.zip -d /usr/local/lib/`

3. Run your application with the following command:

   `LD_LIBRARY_PATH=/usr/local/lib/sdl2 ./YourApplication`
{% endhint %}

Additionally you may need `gpiod`, `libgpiod` and `libgpiod-dev` to use gpio's resources.

