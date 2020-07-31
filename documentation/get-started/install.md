---
description: >-
  How to configure TotalCross to run in any IDE and run your first Hello World
  application
---

# Environment setup

In the next steps of this getting started you will learn how to configure TotalCross and deploy a HelloWorld application to any device on either VSCode, Eclipse, or IntelliJ IDE. Choose the steps you are most comfortable with and get ready to start!

{% hint style="info" %}
You can create your TotalCross applications **from any IDE that supports Java and Maven** projects, but we highly recommend s**tarting with** [**Visual Studio Code**](../miscelaneous/installing-visual-studio-code.md), using the official [TotalCross VSCode plugin](https://marketplace.visualstudio.com/items?itemName=totalcross.vscode-totalcross), as it is a very quick and easy process.
{% endhint %}

{% tabs %}
{% tab title="Visual Studio Code" %}
{% hint style="warning" %}
Please make sure that your Visual Studio Code is updated, as some issues with the plugin may occur on older versions
{% endhint %}

## **Install the TotalCross plugin**

**Step 1:** Open Visual Studio Code and go to _Extensions_.

![Finding the Extensions panel on Visual Studio Code](../../.gitbook/assets/extensions%20%281%29.gif)

**Step 2:** Type TotalCross in the search bar and click to install.

![Installing the TotalCross plugin](../../.gitbook/assets/totalcross.gif)

## Create a Hello World project

**Step 1:** Open VSCode Command Palette \(CTRL + Shift + P on Windows, ⇧⌘**P** on Mac\), type TotalCross and select **TotalCross: Create new Project.**

![Creating a new project](../../.gitbook/assets/create1.gif)

**Step 2:** Create a folder called _HelloWorld_ and select it.

**Step 3:** Fill in the prompted questions. _GroupId_ is the domain of your company domain backward as in `org.wikipedia` for `wikipedia.org`. Feel free to leave it as com.totalcross for this tutorial if you wish.

![Setting up a new project](../../.gitbook/assets/create2.gif)

**Step 4:** ArtifactId is the name of your application, for this example type _HelloWorld_. Select the latest version of TotalCross SDK and choose whatever platform you intend to deploy your application.

![Configuring a new project](../../.gitbook/assets/create3.gif)

**Step 5:** A new window will open with your project. Right click the `RunHelloWorldApplication.java` file inside `src > main > com > totalcross` and choose **Run**. The TotalCross simulator will open with your brand new application.

![](https://gblobscdn.gitbook.com/assets%2F-L_mPP3a_E_A7NbRMq7Q%2F-M2s6FFT1XR5ar8hhLwO%2F-M2sL4EQMLgnZsr7ZB7h%2Fimage.png?alt=media&token=2929d996-d8aa-4395-80a9-55d5f250fb6f)

## Package your application

**Step 1:** Open VSCode _Command Palette_ \(CTRL+Shift+P on Windows, ⇧⌘**P** on Mac\) and search for **TotalCross: Package.**

**Step 2:** When the packaging process is finished the target program will take place inside the folder _target/install/&lt;platform&gt;._

## Deploy and Run you application

{% hint style="warning" %}
Deployment is currently working _**only for linux arm programs**_. This feature performs the implementation and execution of the platform via ssh.
{% endhint %}

**Step 1:** Open VSCode _Command Palette_ \(CTRL + Shift + P on Windows, ⇧⌘**P** on Mac\) and search for **TotalCross: Deploy&Run**. If you just want to deploy, choose the option **TotalCross: Deploy**.

**Step 2:** Fill in the device information.

![](https://gblobscdn.gitbook.com/assets%2F-L_mPP3a_E_A7NbRMq7Q%2F-M29KckxpOSW5OdYicoF%2F-M29MiDCj98COwjMyY1H%2Fdeployplugin.gif?alt=media&token=71c05d7c-525e-4e02-9e67-13900ffbf510)

**Step 3:** See the result on a display connected to your device or with a VNC client.
{% endtab %}

{% tab title="Eclipse" %}
{% hint style="warning" %}
Please make sure that your Eclipse IDE for Java Developers is updated
{% endhint %}

## Clone the HelloWorld repository

**Step 1:** Clone or download [this repository containing a TotalCross HelloWorld application](https://github.com/TotalCross/HelloWorld)

## Import and run the project from Eclipse IDE

**Step 1:** Open the Eclipse IDE and select `File > Import...`

![](../../.gitbook/assets/import_eclipse.gif)

**Step 2:** At the import menu, select `Maven > Existing Maven Projects`

![](../../.gitbook/assets/import_eclipse2.gif)

**Step 3:** Click on `Browse...` __and then select the folder where your _HelloWorld_ repository is located

![](../../.gitbook/assets/import_eclipse3%20%281%29.gif)

**Step 4:** Make sure Eclipse has recognized the _pom.xml_ file and then click `Finish`

![](../../.gitbook/assets/import_eclipse4.gif)

{% hint style="info" %}
Don't worry if Eclipse shows an error about not finding marketplace entries to handle _totalcross-maven-plugin_, it won't have any impact in your project. __But if you want to get rid of it, follow the instructions at the [readme file](https://github.com/TotalCross/HelloWorld/blob/master/README.md) from _HelloWorld_ project to update your _pom.xml_ and fix the problem.
{% endhint %}

**Step 5:** Expand `src/main/java` at the Package Explorer tab, then expand `com.totalcross`, right-click the _RunHelloWordApplication.java_ and choose `Run As > 1. Java Application`. The TotalCross simulator will open with your brand new application.

![](../../.gitbook/assets/import_eclipse5.gif)

## Package your application

**Step** **1:** Right-click the _pom.xml_ file and choose`Run As > 2. Maven Build...` 

![](../../.gitbook/assets/package_eclipse.gif)

**Step** **2:** At the `Goals` text field, type in `clean package`, and then hit `Run`

![](../../.gitbook/assets/package_eclipse2.gif)

**Step 3:** Maven will resolve all the dependencies that you need and build your application for the platforms configured at the _pom.xml_ file. This project is configured by default to build to Android, Linux \(x86\), and Linux\_arm targets. Fell free to remove platforms you don't want and maybe add others such as iOS or Windows. The generated folders will be located inside your repository at `target/install/<platform>`. You can deploy a folder of any platform directly to your target and run your application anywhere!

![](../../.gitbook/assets/package_eclipse3%20%281%29.gif)

{% hint style="info" %}
You can also follow these steps on YouTube:

[Getting Started with TotalCross using Eclipse IDE: Importing a HelloWorld Maven Project](https://youtu.be/J-3EM2eUDPY)
{% endhint %}
{% endtab %}

{% tab title="IntelliJ" %}
{% hint style="warning" %}
Please make sure that your IntelliJ IDE is updated
{% endhint %}

## Clone the HelloWorld repository

**Step 1:** Clone or download [this repository containing a TotalCross HelloWorld application](https://github.com/TotalCross/HelloWorld)

## Import and run the project from IntelliJ IDE

**Step 1:** Open the IntelliJ IDE. From the starting page, select `Open or Import` and open the folder where your _HelloWorld_ repository is located. Open it as a maven project.

![](../../.gitbook/assets/import_intellij.gif)



**Step 2:** To run your application at the TotalCross simulator, expand `HelloWorld/src/main/java` at the Project tab, then expand `com.totalcross`, right-click the _RunHelloWordApplication_ file and choose `Run 'RunHelloApplication.main()'`. The TotalCross simulator will open with your brand new application.

![](../../.gitbook/assets/import_intellij2.gif)

## Package your application

**Step** **1:** Open IntelliJ's maven extension, right-click the option `Lifecycle > package` and choose `Run Maven Build`

![](../../.gitbook/assets/package_intellij.gif)

**Step 2:** Maven will resolve all the dependencies that you need and build you application for the platforms configured at the _pom.xml_ file. This project is configured by default to build to Android, Linux \(x86\), and Linux\_arm targets. Fell free to remove platforms you don't want and maybe add others such as iOS or Windows. The generated folders will be located inside your repository at `target/install/<platform>`. You can deploy a folder of any platform directly to your target and run you application anywhere!

![](../../.gitbook/assets/package_intellij2.gif)

{% hint style="info" %}
You can also follow this steps on YouTube:

[Getting Started with TotalCross using IntelliJ IDE: Importing a HelloWorld Maven Project](https://youtu.be/RqENaIW81oU)
{% endhint %}
{% endtab %}
{% endtabs %}

Now that your environment is ready, let's create the first embedded project in the next session:

{% page-ref page="first-embedded-project-with-totalcross.md" %}



\*\*\*\*

