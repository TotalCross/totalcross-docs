---
description: TotalCross CLI Tool
---

# CLI

With time, most developers grow a preference for their favorite IDE. For that reason we are planning to provide a CLI Tool that can be used with any Java IDE of your choice \(IntelliJ, Eclipse, Netbeans and Visual Studio Code as well\). This CLI Tool will create projects, package, and deploy them. You will aso be able to register and log in as shown bellow.

{% hint style="warning" %}
Be aware that our CLI Tool is its alpha version.
{% endhint %}

### Minimum Requirements

You will need to have installed on your computer:

* [Java 8](https://learn.totalcross.com/get-started/requirements/java-8)
* [Maven](https://learn.totalcross.com/get-started/requirements/maven)
* [Node.js](https://nodejs.org/en/)

### Install TotalCross CLI Tool in 2 steps

{% hint style="danger" %}
**Make sure all dependencies \(Java 8, Maven and Node.js\) are installed on your machine.**
{% endhint %}

**Step 1:** Open your Terminal/CMD/Powershell and type `npm install --global totalcross-npm-cli`.

![Install TotalCross CLI using npm](../../.gitbook/assets/totalcrossinstall.png)

**Step 2:** Verify your installation by typing `totalcross --version`.

![Verifying your installation](../../.gitbook/assets/totalcrossinstallverif.png)

{% hint style="success" %}
Done. TotalCross CLI Toll is successfully installed.
{% endhint %}

### Register in 3 steps

To have access to all features you need a TotalCross account. Create and verify your account in three steps. If you already have a TotalCross account, skip this session.

**Step 1:** Open your Terminal/CMD/Powershell.

**Step 2:** Type `totalcross register` and fill in your information.

![Registration on CLI](../../.gitbook/assets/register3.png)

Step 3: Your account will be created when you fill in all fields. You will receive an email shortly asking you to verify your account. 

{% hint style="success" %}
Your TotalCross account has been created.
{% endhint %}

### Login

**Step 1:** Open your Terminal/CMD/Powershell.

**Step 2:** Type `totalcross login` and enter your email and password used during registration.

![Login on CLI](../../.gitbook/assets/image%20%28124%29.png)

{% hint style="success" %}
Ready! You are logged in.
{% endhint %}

### Hello World

Write your first program.

**Step 1:** Open your Terminal/CMD/Powershell. 

**Step 2:** Type `totalcross create`. You will be asked for the following information that you will be typing into the terminal as they appear.

![](https://gblobscdn.gitbook.com/assets%2F-L_mPP3a_E_A7NbRMq7Q%2F-M24Ghj0M4OeGqwuZzWp%2F-M24JiIWIjVTzDURQX9v%2Fimage.png?alt=media&token=a6421b2a-7016-4f98-81ca-3932662ec8f4)

**Step 3:** After answering the questions, your project will be created and ready to be developed. Type ls to check if your project was created in a folder with the name of the project \(what you entered as project artifactID\).

![](../../.gitbook/assets/image%20%28125%29.png)

### Package

**Step 1:** Open your Terminal/CMD/Powershell

**Step 2:** cd into your project folder

**Step 3:** Run `totalcross package` 

![](../../.gitbook/assets/image%20%28119%29.png)

Step 4: Wait a minute or so. The result of the package will be in the folder `target/install/<platform>`

![](../../.gitbook/assets/image%20%2897%29.png)

### Deploy & Run 

{% hint style="warning" %}
Deploy is working only for _linux arm_ programs. This feature performs the implementation and execution of the platform via ssh.
{% endhint %}

{% tabs %}
{% tab title="CLI" %}
{% hint style="danger" %}
In the version, TotalCross CLI v1.1.2 \(Alpha\), the deploy has been disabled for windows
{% endhint %}

**Step 1:** open your Terminal/CMD/Powershell.

**Step 2:** `cd` into your project folder.

**Step 3:** run `totalcross deploy`, fill in the device information to deploy.

**Step 4:** In `You want to run after deploy ?`, check `yes`, if you just want to deploy choose the `no`.

![](../../.gitbook/assets/image%20%2889%29.png)

  
**Step 5:** see the result on the screen or with VNC
{% endtab %}
{% endtabs %}

{% hint style="success" %}
Now you know how to create, package, deploy and run using TotalCross.
{% endhint %}

### Usage

#### **Commands**

To view detail on any command, use: `totalcross [options] [command]`

* `create`  create new TotalCross project 
* `package` runs mvn package
* `deploy`  deploy your application 
* `login` login into your TotalCross account
* `register`create TotalCross account

**Options:**

* `-V`, `--version` output the version number 
* `-h`, `--help` output usage information

### Feedback

TotalCross CLI is still under active development and we’d love to hear your feedback through [GitLab issues](https://gitlab.com/totalcross/TotalCross/issues/). 





