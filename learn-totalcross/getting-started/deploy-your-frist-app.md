# Deploy Hello World App

## Requierements for deploy

Make sure you have the prerequisites to deploy 

{% page-ref page="../deploy-your-app-android-ios-and-windows/" %}

## **Maven Deploy**

### **Pom File**

In the pom file, we need to add the **properties tags** and the **build tag** as shown in the example below.

```markup
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>com.totalcross.sample</groupId>
    <artifactId>HelloTC</artifactId>
    <version>1.0-SNAPSHOT</version>

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
                                <argument>-linux_arm</argument>
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
    
</project>
```

{% hint style="warning" %}
If you do not have a license for IOS you should remove line 70, 74 and 75
{% endhint %}

### Intellij Idea

**To build the project, you can go to the run menu, and click in edit configurations.**

![](https://lh6.googleusercontent.com/y-5QlWO8feZTwD35Yfz98Rm4dmzYiJS6IqUsF9oQVXV_6haIkPK6kUDuRHN_ElNF2rAK-Kr9OXWJ9vGITiWalJne4MLkPWFdRqpQdyVDXeRBxN6tsZpyDrTgDoMHaRxg3PodUqOY)

**Click in plus button and select Maven.**

![](https://lh5.googleusercontent.com/dNr-EysajY0yKM2W4UNgQnPJ5h87CyDsXe1mcybzYgTP__cqyRVd2rYPWOUWr-Qa_NrZt-YQlhl3q9w8wEyH2LGkjar04C0l9cTpvI_fzaEv703uQUJBg_baFYSSLym4S-HkWvLV)

**In Command Line, add comand "clean package"**

`Clean: Erase the target folder`

`package: Will build the application according to the arguments you put in the pom` 

![](https://lh3.googleusercontent.com/wXzI5MbTzZesGnBeMmMMtPceSqibFNhpFW1Ul5TmRgsLrvkluFmCHXm0yLF0FKIa4uA7cLAezbBbXqj9ulQObxwYXOBA-2W0zyx4V9OodZSvQ6Z1ZNXG0eEjZHLFtiBLGozIJo18)

**After create Maven Build you can run the HelloTC\[clean,package\] for build your app.**

**Just click in run button**

![](https://lh5.googleusercontent.com/AlV6Qq00WXhjaECUgQ9tTHv3N4XGUJhRiNjGoGcUKPrL09HHIEau_NpSse6Zz3uFA1KQKXWnVUT4qI-1ypdhQ1kbXwiIy7XhrodAaltpYGaenw6xExjPFvlegpj9etx1QG7apv-W)

\*\*\*\*

### **Eclipse**

**To build your app you can right click on the project and select Run as -&gt; Maven Build.**

![](https://lh5.googleusercontent.com/fR29G4V17zRnKHcujN6214JZL5N8ZvBAOTW571u-ubKlhamdHo2XG5svOXjB0YgN277D3Glpuyz1ee3MwNYRnWGuEuqjRDakhR3qJbn8FMDzVMUCqYH_sLr0b3Cmc6O2V2ouXaa2)

**Add these arguments in the Goals field: clean package. After this just click in Run;**

`Clean: Erase the target folder`

`package: Will build the application according to the arguments you put in the pom` 

After insert in Goals field, just click in **Run** for build your apps.

![](https://lh5.googleusercontent.com/yJxayDnmrHPyHmH1HCK2_6djrgqwX95dPsULLbSOgLvupFOsKSzb0Ylg9QrFZQpD8KiHxKWh0V5O2Bkcuh1bjc-efbSOY8N3Iy98yBvXtI54I0w01fJlpVMYi0WHykkrh_nnytx7)

![](https://lh5.googleusercontent.com/sZvKD_0mpVyFziejX9WZXjAS62wPjXXgTy3XHVkgHNyO1EoaV9qoXN56FLHWltOIJ6xsblGIr4zpZB_6bxwfSxv2IDv6431xEHNv1viuuDlorFNjBG72g406sTwysJEl-8hqAg2H)

## Your apps

After build your apk It is inside the folder **target\install\** of your project. Sample: **Location\_of\_your\_project\HelloTC\target\install\**  


