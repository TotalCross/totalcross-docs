# Package your app from scratch

## **Requirements**

This guide is intended for devs who have gone through get started or have knowledge of:

* \*\*\*\*[**TotalCross SDK**](http://www.superwaba.net/SDKRegistrationService/)**;**
* [**Environment variables configured**](https://app.gitbook.com/@totalcross/s/playbook/learn-totalcross/getting-started/environment-configuration)**;**
* \*\*\*\*[**JDK installed**](../../miscelaneous/java-8.md)**.**

## Deploy

You can do deploy to Android, iOS e Windows with **Maven** or by **Command Line**

{% tabs %}
{% tab title="Maven" %}
#### Pom File

Make sure your pom file has the **build tag, dependencies tag, repositories tag and properties tag** as shown below

```markup
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>com.totalcross</groupId>
    <artifactId>HelloWorld</artifactId>
    <version>1.0-SNAPSHOT</version>
    <name>HelloWorld</name>

    <properties>
        <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
        <totalcross.activation_key>PLACE_YOUR_KEY</totalcross.activation_key>
    </properties>

    <dependencies>
        <dependency>
            <groupId>com.totalcross</groupId>
            <artifactId>totalcross-sdk</artifactId>
            <version>6.0.3</version>
        </dependency>
    </dependencies>

    <repositories>
        <repository>
            <id>totalcross-repo</id>
            <name>ip-172-31-40-140-releases</name>
            <url>http://maven.totalcross.com/artifactory/repo1</url>
        </repository>
    </repositories>

    <pluginRepositories>
        <pluginRepository>
            <id>totalcross-repo</id>
            <name>ip-172-31-40-140-releases</name>
            <url>http://maven.totalcross.com/artifactory/repo1</url>
        </pluginRepository>
    </pluginRepositories>

    <build>
        <finalName>${project.artifactId}</finalName>
        <plugins>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-compiler-plugin</artifactId>
                <version>3.1</version>
                <configuration>
                    <source>1.8</source>
                    <target>1.8</target>
                </configuration>
            </plugin>
            <plugin>
                <groupId>com.totalcross</groupId>
                <artifactId>totalcross-maven-plugin</artifactId>
                <version>1.0</version>
                <configuration>
                    <name>${project.name}</name>
                    <platforms>
                        <platform>-win32</platform>
                        <platform>-android</platform>
                        <platform>-ios</platform>
                    </platforms>
                    <activationKey>${totalcross.activation_key}</activationKey>
                    <!--                    For version 4.4.2 and 5.1.4 or later, Apple certificates are no longer required. -->
                    <!--                    <certificates>${totalcross.applecertificate}</certificates>-->
                    <!--                    <totalcrossHome>/Users/italo/TotalCross5</totalcrossHome>-->
                </configuration>
                <executions>
                    <execution>
                        <id>post-package</id>
                        <phase>package</phase>
                        <goals>
                            <goal>package</goal>
                        </goals>
                    </execution>
                </executions>
            </plugin>
        </plugins>
    </build>
</project>
```

Inside the **platfrom tag** you can add the argument:

#### Argument for plataforms to deploy

* `<platform>-win32</platform>`This platform is used to build for **Windows**;
* `<platform>-wince</platform>`This platform is used to build for **Windows CE**;
* `<platform>-winmo</platform>`This platform is used to build for **Windows Mobile Only;**
* `<platform>-linux</platform>`This platform is used to build for **Linux x86 \(Debian\);**
* `<platform>-linux_arm</platform>`This platform is used to build for **Linux ARM**;
* `<platform>-applet</platform>`Create the html file and a jar file with all dependencies   to run the app from a java-enabled browser \(the input cannot be a jar file\);
* `<platform>-ios</platform>`This platform is used to build for **IOS**;
* `<platform>-android</platform>`This platform is used to build for **Android**;
* `<platform>-all</platform>`Single parameter to deploy to all supported platforms;

#### Options

* `<platform>/p</platfrom>`Package the **VM** with the application;
* `<platform>/r</platform>`Specify a **registration key** to be used to activate TotalCross when required;
* `<platform>/m</platform>`**Specifies a path** to the mobileprovision and **certificate store** to deploy an ipa file for iOS;
* `<platform>/a</platform>`Assigns the application id; can only be used for libraries or passing a .tcz file;
* `<platform>/autostart</platform>`automatically starts the application after a boot is completed. Currently works for Android only;
* `<platform>/c</platform>`Specify a command line to be passed to the application;
* `<platform>/i</platform>`Install the file after generating it; platforms is a list of comma-separated platforms. Supports: android. E.G.: /i android;
* `<platform>/k</platform>`Keep the .exe and other temporary files during wince generation;
* `<platform>/kn</platform>`As /k, but does not create the cab files for WinCE;
* `<platform>/n</platform>`Override the name of the tcz file with the given name;
* `<platform>/o</platform>` ****Override the output folder with the given path \(defaults to the current folder\);
* `<platform>/t</platform>`Just test the classes to see if there are any invalid references. Images are not converted, and nothing is written to disk;
* `<platform>/v</platform>`Verbose output for information messages;
* `<platform>/w</platform>`Waits for a key press if an error occurs;
* `<platform>/x</platform>`Comma-separated list of class names that must be excluded \(in a starts-with manner\). E.G.: "/x com/framework/".

#### Build your app

To deploy your application you only need to use a maven execution template by passing the command:`mvn package`
{% endtab %}

{% tab title="Command Line" %}
To deploy by command line you need to be in the folder that contains the jar of your project and pass the parameters of tc.Deploy:

#### Argument for plataforms to deploy

* `-win32`This argument is used to build for **Windows**;
* `-wince`This argument is used to build for **Windows CE**
* `-winmo` This argument is used to build for **Windows Mobile Only;**
* `-linux` This argument is used to build for **Linux x86 \(Debian\)**;
* `-linux_arm` This platform is used to build for **Linux ARM**;
* `-applet` the html file and a jar file with all dependencies to run the app from a java-enabled browser \(the input cannot be a jar file\);
* `-ios`This argument is to build for **iOS**;
* `-android`This argument is to build for **Android**;
* `-all`Single parameter to deploy to all supported platforms;

#### Options

* `/p`Package the **VM** with the application;
* `/r`Specify a **registration key** to be used to activate TotalCross when required;
* `/m`**Specifies a path** to the mobileprovision and **certificate store** to deploy an ipa file for iOS;
* `/a`Assigns the application id; can only be used for libraries or passing a .tcz file;
* `/autostart`automatically starts the application after a boot is completed. Currently works for Android only;
* `/c` Specify a command line to be passed to the application;
* `/i`install the file after generating it; platforms is a list of comma-separated platforms. Supports: android. E.G.: /i android;
* `/k`Keep the .exe and other temporary files during WinCE generation;
* `/kn`As /k, but does not create the cab files for WinCE;
* `/n` Override the name of the .tcz file with the given name;
* `/o` ****Override the output folder with the given path \(defaults to the current folder\);
* `/t` Just test the classes to see if there are any invalid references. Images are not converted, and nothing is written to disk;
* `/v`Verbose output for information messages;
* `/w` Waits for a key press if an error occurs;
* `/x`Comma-separated list of class names that must be excluded \(in a starts-with manner\). E.G.: "/x com/framework/".

#### See the example below

`java -cp "%TOTALCROSS3_HOME%"/dist/totalcross-sdk.jar tc.Deploy HelloTC.jar -android /p /r YOUR_TC_KEY_HERE`

`"%TOTALCROSS3_HOME%"`  is the folder where the TC SDK

`HelloTC.jar` is the .jar of project
{% endtab %}
{% endtabs %}

## Your apps

After packaging your application the files will be in the `project_folder\target\install\`

{% hint style="danger" %}
Problems with WinCE? If your Operational System is not Windows or it is Windows and has not Cabwiz program, try to add`/k`as first platform to  in your pom.xml
{% endhint %}

