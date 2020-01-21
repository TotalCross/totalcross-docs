# Deploy your app with a dependecy TC

In this tutorial we will use the repository [https://github.com/TotalCross/tc-utilities](https://github.com/TotalCross/tc-utilities)

## Download Dependecy

‌You need to add in your pom file within your dependencies tag the dependency:

{% code title="Dependecy Example" %}
```text
<dependencies>
    .
    .
    .
    <dependency>
        <groupId>com.totalcross.utils</groupId>
        <artifactId>tc-utilities</artifactId>
        <version>0.0.1-SNAPSHOT</version>
    </dependency>
    
</dependencies>
```
{% endcode %}

## Generate TCZ

After downloading the dependency it will be necessary to generate the tcz of the dependency so that it is included in the deploy

Find the folder you extracted the project from or if you have downloaded it by pom that is located in the dependency, usually is: C:\Users\**your\_user**\.m2\repository\com\totalcross\utils\tc-utilities\0.0.1-SNAPSHOT.

![](https://blobscdn.gitbook.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-L_mPP3a_E_A7NbRMq7Q%2F-Ler5cEPPNSBJ9P-W-mI%2F-Ler7XyzuHa5LexKKFId%2FPasta.PNG?alt=media&token=a45e3908-5361-4bca-adb5-fc79b3590c54)

To generate tcz execute the command java -cp "% TOTALCROSS 3\_HOME%" / dist / totalcross-sdk.jar tc.Deploy tc-utilities-0.0.1-SNAPSHOT.jar / r YOUR\_TC\_KEY‌

![](https://blobscdn.gitbook.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-L_mPP3a_E_A7NbRMq7Q%2F-LerIfBrCEJKzx7OT0xZ%2F-LerIl475Yrmu5dtoeFU%2FComp.PNG?alt=media&token=b491c16a-dba7-4c53-8e68-16c90e5e2a50)

After tcz is generated, rename the tc-utilities-0.0.1-SNAPSHOT.tcz file to tc-utilities-0.0.1-SNAPSHOTLib.tcz and place it at the root of the project.‌

At the root of the project create the file named **all.pkg** and put \[L\] tc-utilities-0.0.1-SNAPSHOTLib.tcz so that this class is included in deploy

![](https://blobscdn.gitbook.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-L_mPP3a_E_A7NbRMq7Q%2F-Ler5cEPPNSBJ9P-W-mI%2F-LerEHwNAfZIsaPx7r-N%2F1.1.png?alt=media&token=4b4ad9a8-3f97-494e-89e1-46f16db4172e)

