# Deploy Your App

## **Requirements for Deploy**

* \*\*\*\*[**TotalCross SDK** ](http://www.superwaba.net/SDKRegistrationService/)
* [**environment variables configured**](https://app.gitbook.com/@totalcross/s/playbook/learn-totalcross/getting-started/environment-configuration)
* [**JDK installed**](https://app.gitbook.com/@totalcross/s/playbook/learn-totalcross/getting-started/basic-requirements)\*\*\*\*

## Deploy

You can do deploy to Android, iOS e Windows with **maven** or by **command line**

### Maven

#### Pom File

Make sure your pom file has the **build tag, dependencies tag, repositories tag and properties tag** as shown below

```markup
    <properties>
        <totalcross.activation_key>PLACE_YOUR_KEY_HERE</totalcross.activation_key>
    </properties>

    <dependencies>
        <dependency>
            <groupId>com.totalcross</groupId>
            <artifactId>totalcross-sdk</artifactId>
            <version>5.0.1</version>
        </dependency>
    </dependencies>
    <repositories>
        <repository>
            <id>totalcross-repo</id>
            <name>ip-172-31-40-140-releases</name>
            <url>http://maven.totalcross.com/artifactory/repo1</url>
        </repository>
    </repositories>

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
                <groupId>net.orfjackal.retrolambda</groupId>
                <artifactId>retrolambda-maven-plugin</artifactId>
                <version>2.5.1</version>
                <executions>
                    <execution>
                        <goals>
                            <goal>process-main</goal>
                        </goals>
                    </execution>
                </executions>
            </plugin>
            <plugin>
                <groupId>org.codehaus.mojo</groupId>
                <artifactId>exec-maven-plugin</artifactId>
                <version>1.1.1</version>
                <executions>
                    <execution>
                        <phase>package</phase>
                        <goals>
                            <goal>java</goal>
                        </goals>
                        <configuration>
                            <mainClass>tc.Deploy</mainClass>
                            <arguments>
                                <argument>${project.build.directory}/${project.build.finalName}.${project.packaging}</argument>
                                <argument>-win32</argument>
                                <argument>-android</argument>
                                <argument>-ios</argument>
                                <argument>/p</argument>
                                <argument>/r</argument>
                                <argument>${totalcross.activation_key}</argument>
                                <argument>/m</argument>
                                <argument>{put ios certificate path here}</argument>
                            </arguments>
                        </configuration>
                    </execution>
                </executions>
            </plugin>
        </plugins>
    </build>
```

{% hint style="warning" %}
If you do not have a license for IOS you should remove line 45, 49 and 50.
{% endhint %}

Inside the **argument tag** you can add the argument:

#### Argument for plataforms to deploy

* `<argument>-win32</argument>`This argument is to build for **windows**;
* `<argument>-wince</argument>`This argument is to build for **windows CE**;
* `<argument>-winmo</argument>`This argument is to build for **windows Mobile Only**;
* `<argument>-linux</argument>`This argument is to build for **linux**;
* `<argument>-applet</argument>`create the html file and a jar file with all dependencies

         to run the app from a java-enabled browser \(the input cannot be a jar file\);

* `<argument>-android</argument>`This argument is to build for **android**;
* `<argument>-ios</argument>`This argument is to build for **iOS**;
* `<argument>-linux_arm</argument>`This argument is to build for **RaspiberryPI**;
* `<argument>-all</argument>`single parameter to deploy to all supported platforms;

#### Options

* `<argument>/p</argument>`Package the **VM** with the application;
* `<argument>/r</argument>`Specify a **registration key** to be used to activate TotalCross when required;
* `<argument>/m</argument>`**Specifies a path** to the mobileprovision and **certificate store** to deploy an ipa file for iOS.
* `<argument>/a</argument>` Assigns the application id; can only be used for libraries or passing a tcz file
* `<argument>/autostart</argument>`automatically starts the application after a boot is completed. Currently works for Android only.
* `<argument>/c</argument>` Specify a command line to be passed to the application
* `<argument>/i</argument>`  install the file after generating it; platforms is a list of comma-separated platforms. Supports: android. E.G.: /i android
* `<argument>/k</argument>` Keep the exe and other temporary files during wince generation
* `<argument>/kn</argument>`As /k, but does not create the cab files for wince
* `<argument>/n</argument>` Override the name of the tcz file with the given name
* `<argument>/o</argument>` ****Override the output folder with the given path \(defaults to the current folder\)
* `<argument>/t</argument>` Just test the classes to see if there are any invalid references. Images are not converted, and nothing is written to disk.
* `<argument>/v</argument>` Verbose output for information messages
* `<argument>/w</argument>` Waits for a key press if an error occurs
* `<argument>/x</argument>` Comma-separated list of class names that must be excluded \(in a starts-with manner\). E.G.: "/x com/framework/"

#### Build your app

To deploy your application you only need to use a maven execution template by passing the `command: package`

### Command line

to deploy by command line you need to be in the folder that contains the jar of your project and pass the parameters of tc.deploy

#### Argument for plataforms to deploy

* `-win32`This argument is to build for **windows**;
* `-wince` This argument is to build for **windows CE**
* `-winmo` argument is to build for **windows Mobile Only;**
* `-linux` argument is to build for **linux**;
* `-applet` the html file and a jar file with all dependencies to run the app from a java-enabled browser \(the input cannot be a jar file\);
* `-android`This argument is to build for **android**;
* `-ios`This argument is to build for **iOS**;
* `-all`single parameter to deploy to all supported platforms;

#### Options

* `/p`Package the **VM** with the application;
* `/r`Specify a **registration key** to be used to activate TotalCross when required;
* `/m`**Specifies a path** to the mobileprovision and **certificate store** to deploy an ipa file for iOS.
* `/a`Assigns the application id; can only be used for libraries or passing a tcz file
* `/autostart`automatically starts the application after a boot is completed. Currently works for Android only.
* `/c` Specify a command line to be passed to the application
* `/i`install the file after generating it; platforms is a list of comma-separated platforms. Supports: android. E.G.: /i android
* `/k`Keep the exe and other temporary files during wince generation
* `/kn`As /k, but does not create the cab files for wince
* `/n` Override the name of the tcz file with the given name
* `/o` ****Override the output folder with the given path \(defaults to the current folder\)
* `/t` Just test the classes to see if there are any invalid references. Images are not converted, and nothing is written to disk.
* `/v`Verbose output for information messages
* `/w` Waits for a key press if an error occurs
* `/x`Comma-separated list of class names that must be excluded \(in a starts-with manner\). E.G.: "/x com/framework/"

#### See the example below

`java -cp "%TOTALCROSS3_HOME%"/dist/totalcross-sdk.jar tc.Deploy HelloTC.jar -android /p /r YOUR_TC_KEY_HERE`

`"%TOTALCROSS3_HOME%" = is the folder where the TC SDK`

`HelloTC.jar = is the jar of project`

### Your apps

After building your application the files will be in the `project_folder\target\install\`

