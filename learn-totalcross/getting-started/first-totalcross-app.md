# Hello World App

## About this tutorial

On this tutorial we will create a simple Hello World project, where we will have a label being changed by a button event

The tutorial will be divided into two sections

[Intellij IDE](https://totalcross.gitbook.io/playbook/~/drafts/-La_2CQv07ad2w8y5f3J/primary/learn-totalcross/getting-started/your-first-totalcross-app#intellij-ide) and [Eclipse](https://totalcross.gitbook.io/playbook/~/drafts/-La_2CQv07ad2w8y5f3J/primary/learn-totalcross/getting-started/your-first-totalcross-app#eclipse)

## Intellij IDE

### Create a new project

![](../../.gitbook/assets/image%20%2855%29.png)

Click in `Create New Project`, select Maven and click in next

![](../../.gitbook/assets/image%20%2849%29.png)

Put this data: `GroupId = com.totalcross.sample` , `ArtifactId = HelloTC` in whitespace and click in next.

![](../../.gitbook/assets/image%20%2845%29.png)

In `Project Location` place the directory of your choice, after this, click in finish

![](../../.gitbook/assets/image%20%2836%29.png)

#### TotalCross Sources and JavaDocs

In order, to make your development easier, Go to: `Preference > Build, Execution and Deployment > Build Tools > Maven > Importing.` and mark options Automatically Download Sources and Documentation. As shown in the Figure bellow:

![](../../.gitbook/assets/image%20%2851%29.png)

Click Ok in the Preferences panel and proceed to the next steps.

### Project

#### Structures

You need to leave the structure of your project the same as the example below.

To add new package you have to right-click in Java package  **select new -&gt; package**

```text
└── src
    └── main
        └── java
            └── com
                └── totalcross
                    └── sample
                        └── HelloTC

```

![](../../.gitbook/assets/image%20%2863%29.png)

In the **pom.xml** file, add the following code snippet to the file inside the  **project tag**.

```markup
<properties>
    <maven.compiler.source>1.8</maven.compiler.source>
	<maven.compiler.target>1.8</maven.compiler.target>
</properties>

<dependencies>
	<dependency>
		<groupId>com.totalcross</groupId>
		<artifactId>totalcross-sdk</artifactId>
		<version>5.0.0</version>
	</dependency>
</dependencies>
<repositories>
	<repository>
		<id>totalcross-repo</id>
		<name>ip-172-31-40-140-releases</name>
		<url>http://maven.totalcross.com/artifactory/repo1</url>
	</repository>
</repositories>

```

{% hint style="warning" %}
After this, you need import the pom file changes

![](../../.gitbook/assets/image%20%285%29.png)
{% endhint %}

{% hint style="warning" %}
Remember the download dependencies may take according to your internet :D
{% endhint %}

### Creating Classes

To create classes, you have to do right click in package **sample** and select **new -&gt; java class.**

{% hint style="warning" %}
Beware classes begin with the first capital letter
{% endhint %}

#### Create HelloTC

![](../../.gitbook/assets/image%20%2814%29.png)

#### Create HelloTCApplication

![](../../.gitbook/assets/image%20%2838%29.png)

### Add Code

#### Class HelloTC

This class will be responsible for mounting the screen.

```java
package com.totalcross.sample.HelloTC;

import totalcross.ui.Button;
import totalcross.ui.Label;
import totalcross.ui.MainWindow;

public class HelloTC extends MainWindow {

    @Override
    public void initUI() {
         Label label = new Label("Hello World");
        add(label,CENTER,TOP + 50);

        Button button = new Button("Click Here");
        button.addPressListener(e->{
            label.setText("Hello Totalcross");
            label.reposition();
        });
        add(button, SAME, CENTER);

    }
}

```

#### Class HelloTCApplication

This class will be responsible for start your project.

```java
package com.totalcross.sample.HelloTC;

import totalcross.TotalCrossApplication;

public class HelloTCApplication {
    public static void main(String[] args) {
        TotalCrossApplication.run(HelloTC.class,
                "/r",
                "PLACE_YOUR_KEY_HERE");
    }
}

```

{% hint style="warning" %}
Be sure the put your TotalCross Key in line 9
{% endhint %}

### Run Project

To start your application you can righ-click on class HelloTCApplication and click in Run.

{% hint style="info" %}
Take a look at the section below for more details about the TotalCross Simulator 

{% page-ref page="../device-simulator.md" %}
{% endhint %}

![](../../.gitbook/assets/image%20%2853%29.png)



## Eclipse 

### Create a new project

Click in **file -&gt; new -&gt; Maven Project**

![](../../.gitbook/assets/image%20%2833%29.png)

Just click **Next** 

![](../../.gitbook/assets/image%20%2847%29.png)

Select the column `Artifact Id maven-archetype-quickstart` and click in **Next**.

![](../../.gitbook/assets/image%20%2868%29.png)

Put this data in `Group id = com.totalcross.sample` and `Artifact id = HelloTC`, after this click in finish.

![](../../.gitbook/assets/image%20%2828%29.png)

### Project

![](../../.gitbook/assets/image%20%2842%29.png)

In the pom file, add the following code snippet in line 13 replacing the current contents of the file.

```markup
<properties>
    <maven.compiler.source>1.8</maven.compiler.source>
	<maven.compiler.target>1.8</maven.compiler.target>
</properties>

<dependencies>
	<dependency>
		<groupId>com.totalcross</groupId>
		<artifactId>totalcross-sdk</artifactId>
		<version>5.0.0</version>
	</dependency>
</dependencies>
<repositories>
	<repository>
		<id>totalcross-repo</id>
		<name>ip-172-31-40-140-releases</name>
		<url>http://maven.totalcross.com/artifactory/repo1</url>
	</repository>
</repositories>

```

{% hint style="warning" %}
Remember the download dependencies may take according to your internet :D
{% endhint %}

### Creating Classes

To create classes, you have to do right click in package HelloTC e select **new -&gt; other...**

![](../../.gitbook/assets/image%20%2825%29.png)

{% hint style="warning" %}
Beware classes begin with the first capital letter
{% endhint %}

#### Create HelloTC

![](../../.gitbook/assets/image%20%2860%29.png)

### Add Code

#### Class HelloTC

This class will be responsible for mounting the screen.

```java
package com.totalcross.sample.HelloTC;

import totalcross.ui.Button;
import totalcross.ui.Label;
import totalcross.ui.MainWindow;

public class HelloTC extends MainWindow {

    @Override
    public void initUI() {
         Label label = new Label("Hello World");
        add(label,CENTER,TOP + 50);

        Button button = new Button("Click Here");
        button.addPressListener(e->{
            label.setText("Hello Totalcross");
            label.reposition();
        });
        add(button, SAME, CENTER);

    }
}

```

#### Class App

This class will be responsible for start your project.

```java
package com.totalcross.sample.HelloTC;

import totalcross.TotalCrossApplication;

public class App{
    public static void main(String[] args) {
        TotalCrossApplication.run(HelloTC.class,
                "/r",
                "PLACE_YOUR_KEY_HERE");
    }
}

```

{% hint style="warning" %}
Be sure the put your TotalCross Key in line 9
{% endhint %}

### Run Project

To start your application you can righ-click on **class App** and select **Run as -&gt; 1 Java Application**

![](../../.gitbook/assets/run.png)

