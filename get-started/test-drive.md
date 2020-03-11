---
description: Test that the Totalcross SDK is installed correctly
---

# 3. Test Drive

## Register

To have access to all features of these tools you need to have a TotalCross account!

{% tabs %}
{% tab title="VS Code" %}
**Step 1:** open VS Code terminal _CTRL+SHIFT+P_ and search _TotalCross_:

![](../.gitbook/assets/register1.gif)

**Step 2:** select _TotalCross: Register_ option and fill in the fields with your information:

![](../.gitbook/assets/register2.gif)
{% endtab %}

{% tab title="CLI Tool" %}
**Step 1:** open your Terminal/CMD/Powershell

**Step 2:** type `totalcross register` and you will be asked for some information about yourself. 

![](../.gitbook/assets/image%20%281%29.png)
{% endtab %}
{% endtabs %}

{% hint style="success" %}
After complete, your account will be created!
{% endhint %}

## Login

You can now login!

{% tabs %}
{% tab title="VS Code" %}
**Step 1:** open VS Code _Command Palette_ \(_CTRL+Shift+P_\) and search _TotalCross_:

![](../.gitbook/assets/register1.gif)

**Step 2:** select _TotalCross: Login_ option and fill in the fields with your information:

![](../.gitbook/assets/login%20%281%29.gif)
{% endtab %}

{% tab title="CLI Tool" %}
**Step 1:** open your Terminal/CMD/Powershell

**Step 2:** run `totalcross login` then write your e-mail and password already registered. 

![](../.gitbook/assets/image%20%2873%29.png)
{% endtab %}
{% endtabs %}

{% hint style="success" %}
Ready! You are logged in.
{% endhint %}

## Create

Creating your first application is really simple and straightforward. Once you have accomplished all the basic requirements, you will be able to run your first application in about 5 minutes. Thus, choose the environment that makes you feel more comfortable:

{% tabs %}
{% tab title="VS Code" %}
**Step 1:** open VS Code _Command Palette_ \(_CTRL+Shift+P_\) and type _TotalCross_ autocomplete should help! Select _TotalCross: Create new Project._ Then __create a folder called _HelloWorld_ and select it.

![](../.gitbook/assets/create1.gif)

**Step 2:** _GroupId_ will be `com.totalcross`, but you can replace with the name of your company \(as you would chose a domain for your company backwards, example: `org.wikipedia` for `wikipedia.org`\).

![](../.gitbook/assets/create2.gif)

**Step 3:** _ArtifactId is the name of your application, in this example it_ will be `HelloWorld`. Select the latest version of TotalCross SDK and choose whatever platform you intend to deploy an application.

![](../.gitbook/assets/create3.gif)

**\(Optional\)** A new window with the new project structure will be open. Right click on the`RunHelloWorldApplication.java` inside `src> main> com> totalcross` and choose click _Run_ \(IDE\). This will make your new application run on our Java simulator:
{% endtab %}

{% tab title="CLI Tool" %}
**Step 1:** open your Terminal/CMD/Powershell

**Step 2:** run `totalcross create` and you will be asked for the following information that you will be typing into the terminal as they appear.

![](../.gitbook/assets/image%20%2886%29.png)

**Step 3:** after answering the questions, your project will be created and ready to be developed. You can give a `ls` in the terminal to check if your project was created in a folder with the name of the project.

![](../.gitbook/assets/image%20%2861%29.png)
{% endtab %}
{% endtabs %}

{% hint style="success" %}
Now you know how to create TotalCross projects
{% endhint %}

## Package

As Totalcross is a cross platform SDK, packaging is one of the most important phases in the development process. Using Totalcross, you can deliver application for the following platform.

{% tabs %}
{% tab title="VS Code" %}
**Step 1:** open VS Code _Command Palette_ \(_CTRL+Shift+P_\) and search for _TotalCross_: _Package_

**Step 2:** after the package process is finished the target program will take place inside the folder _target/install/&lt;platform&gt;_
{% endtab %}

{% tab title="CLI" %}
**Step 1:** open your Terminal/CMD/Powershell

**Step 2:** `cd` into your project folder:

**Step 3:** run `totalcross package` :

![](../.gitbook/assets/image%20%2829%29.png)

**Step 4:** wait a minute. The result of the package will be in the folder `target/install/<platform>`

![](../.gitbook/assets/image%20%2850%29.png)
{% endtab %}
{% endtabs %}

{% hint style="success" %}
Now you know how to package TotalCross projects!
{% endhint %}

## Deploy

In addition, you can still deploy in an uncomplicated way, in the environment you want.

{% hint style="warning" %}
Deploy is working only for _linux arm_ programs. This feature performs the implementation and execution of the platform via ssh.
{% endhint %}

{% tabs %}
{% tab title="VS Code" %}
**Step 1:** open VS Code _Command Palette_ \(_CTRL+Shift+P_\) and search for _TotalCross_: _Deploy_

**Step 2:** fill in the device information to deploy.

![](../.gitbook/assets/deployplugin%20%281%29.gif)

**Step 3:** see the result on the screen or with VNC
{% endtab %}

{% tab title="CLI" %}
**Step 1:** open your Terminal/CMD/Powershell

**Step 2:** `cd` into your project folder

**Step 3:** run `totalcross deploy`, fill in the device information to deploy.

![](../.gitbook/assets/image%20%2875%29.png)
{% endtab %}
{% endtabs %}

{% hint style="success" %}
You've learnt how to create a new project, package and deploy.  
{% endhint %}



