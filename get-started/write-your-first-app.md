---
description: Running your first application in TotalCross.
---

# 3. Your first app



## Creating Your First Application \(Hello World\)

Creating your first application is really simple and straightforward. Once you have accomplished all the basic requirements, you will be able to run your first application in about 5 minutes. Thus, choose the environment that makes you feel more comfortable:

{% tabs %}
{% tab title="VS Code" %}
Install our plugin for VS Code: [TotalCross extension for VS Code](https://marketplace.visualstudio.com/items?itemName=Italo.totalcross). 

After having the plugin installed, open VS Code console  \(CTRL + Shift + P\) and type TotalC… autocomplete should help!

![](../.gitbook/assets/3-1.gif)

Select _TotalCross: Create new Project._ Then __create a folder called _HelloWorld_ and select it. _GroupId_ will be `com.totalcross`, but you can replace with the name of your company \(as you would chose a domain for your company backwards, example: `org.wikipedia` for `wikipedia.org`\). _ArtifactId is the name of your application, in this example it_ will be `HelloWorld`. Select the latest version of TotalCross SDK and choose whatever platform you intend to deploy an application.

![Click to expand](../.gitbook/assets/4-1.gif)

A new window with the new project structure will be open. Right click on the`RunHelloWorldApplication.java` inside `src> main> com> totalcross` and choose click _Run_ \(IDE\). This will make your new application run on our Java simulator:

![Click  to expand](../.gitbook/assets/5-1.gif)
{% endtab %}

{% tab title="CLI" %}
{% hint style="warning" %}
The TotalCross CLI tool is under development. But don't worry, our awesome development team are going to get this done in the first week of february 2020 😁 . 
{% endhint %}
{% endtab %}
{% endtabs %}

## Packaging

As Totalcross is a cross platform SDK, packaging is one of the most important phases in the development process. Using Totalcross, you can deliver application for the following platform.

{% tabs %}
{% tab title="VS Code" %}
With the project open in VS Code, open the _Command Palette_ `F1` or `(CTRL + Shift + P)` and search for `Totalcross: Package`; 

After the package process is finished the target program will take place inside the folder `target/install/<platform>`.

![](../.gitbook/assets/diize1x.gif)
{% endtab %}

{% tab title="CLI" %}
{% hint style="warning" %}
The TotalCross CLI tool is under development. But don't worry, our awesome development team are going to get this done in the first week of february 2020 😁 . 
{% endhint %}
{% endtab %}
{% endtabs %}

## Deploy

In addition, you can still deploy in an uncomplicated way, in the environment you want.

{% tabs %}
{% tab title="VS Code" %}
In VS Code the deploy is working only for linux arm programs. This feature performs the implementation and execution of the platform via ssh.

To do it open the project and press `F1` or `(CTRL + Shift + P)` and search for `Totalcross: Deploy&Run`.

![](../.gitbook/assets/y6f3ptc.gif)
{% endtab %}

{% tab title="CLI" %}
{% hint style="warning" %}
The TotalCross CLI tool is under development. But don't worry, our awesome development team are going to get this done in the first week of february 2020 😁 . 
{% endhint %}
{% endtab %}
{% endtabs %}

{% hint style="success" %}
You've learnt how to create a new project, package and deploy.  
{% endhint %}



