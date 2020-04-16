---
description: April to June
---

# Roadmap

## Overview

Our roadmap shares our current **focus**: what we are presently working on and what is our scope for **this quarter**. It is a reflection of our ongoing strategic plan, so content _can be changed at any time_, due to **users** demands or strategic impact for business.

## What's coming?

Please, feel free to contribute with your questions or suggestions for each topic via [github](https://github.com/TotalCross/totalcross/issues?q=is%3Aissue+is%3Aopen+label%3AFeature). We have lively discussions happening there.

### Highlights

#### External and native libraries

One of TotalCross developers most requested features is the possibility of using native and external libraries within their applications. This functionality is extremely important for several reasons, among them being able to use serial ports like RS232, access peripherals, and perform hardware analysis. It is our number one priority.

To implement this, we divided it into two macro activities: 

* create a new method based on the [runtime.exec of java](https://docs.oracle.com/javase/7/docs/api/java/lang/Runtime.html#exec%28java.lang.String%29); 
* Improve **TCNI** for community use;

{% hint style="info" %}
TCNI is a foreign function interface programming framework that enables TotalCross/Java code running in a Java virtual machine to call and be called by native applications and libraries written in other languages such as C, C ++ and assembly.\)
{% endhint %}

Click here to reach this topic on [github](https://github.com/TotalCross/totalcross/issues/1).

#### Organize TCVM, TC API Java and Litebase in different repositories on github

From version 6 [TotalCross SDK is open source](https://github.com/TotalCross/totalcross/). Our goal is to make contributing the simplest, facilitating the understanding of what makes up the TC SDK.

Click here to reach this topic on [github](https://github.com/TotalCross/totalcross/issues/2).

#### **Nightly builds**

Continuous integration is an important point and we are working to implement it more and more. 

We will start with [nightly builds](https://blog.testproject.io/2019/10/14/what-are-the-benefits-of-having-nightly-builds/), a feature that consists of automatically generating realizations during the night, avoiding wait by TotalCross users for the release of [minor ](https://semver.org/)versions to access implemented fixes and features.

Click here to reach this topic on [github](https://github.com/TotalCross/totalcross/issues/3).

#### Documentation

We know that there is no point in having incredible features if developers don't know they exist and how to use them. So now there is a team of developers focused on producing documentation, guides and articles. 

Feel free to contribute with your suggestions creating an [issue on GitHub](https://github.com/TotalCross/totalcross/labels/documentation).

### **Others**

Click on the item to be directed to the github discussion**.**

* [Custom Cam; ](https://github.com/TotalCross/totalcross/issues/6)
* [Sharing information between apps for Android and iOS;](https://github.com/TotalCross/totalcross/issues/11)
* [Improve error warnings in the VSCode plugin and CLI;](https://github.com/TotalCross/totalcross/issues/10)
* [Allow using the camera via streaming;](https://github.com/TotalCross/totalcross/issues/9)
* [Add Lambda](https://github.com/TotalCross/totalcross/issues/5);
* Have publics dists of [totalcross-yocto](https://github.com/TotalCross/totalcross/issues/7) and [totalcross-torizon](https://github.com/TotalCross/totalcross/issues/8);
* [Allow registration and login with GitHub on TotalCross](https://github.com/TotalCross/totalcross/issues/4);









