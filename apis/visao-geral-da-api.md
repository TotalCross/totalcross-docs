---
description: Short description about the Totalcross API
---

# API Overview

## **TotalCross Packages**

### totalcross.crypto

The classes used by TotalCross to work with encryption are: 

* **Cipher**: AES e RSA;
* **Digest**: MD5, SHA1, SHA256 ;
* **Signature**: PKCS1.

### totalcross.db e totalcross.sql

The **totalcross.db** package has SQLite Java implementation, the most widely used portable database in the world. Allows you to use SQL commands to manipulate data files lightly and with low memory consumption.

The t**otalcross.sql** package has JDBC implementation for use with SQLite - SQLiteUtil - as you can see in the code example below:

```java
public class DatabaseManager {

	public static SQLiteUtil sqliteUtil;

	static {
		try {
			sqliteUtil = new SQLiteUtil(Settings.appPath, "test.db");
			Statement st = sqliteUtil.con().createStatement();
			st.execute("create table if not exists person (cpf varchar)");
			st.close();

		} catch (SQLException e) {
			e.printStackTrace();
		}
	}
}
```

To learn more about SQLite, how to implement SQLite Useful, creating applications with database and CRUD just read the link session below:

{% page-ref page="../learn-totalcross/how-to-store-data-sqlite.md" %}

### totalcross.io

The totalcross.io package concentrates the classes used in input and output.

* ByteArrayStream
* DataStream 
* File 
  * BufferedStream 
* LineReader 
* device.bluetooth 
* device.gps 
* device.printer 
* device.scanner

### totalcross.json

In this class we have the json library in Java, a lot used in the creation of Web Services through Rest. To understand better, visit the session below:

{% page-ref page="json.md" %}

### totalcross.map

Totalcross.map supports GoogleMaps and Waze. You can better understand by clicking on the session below:

{% page-ref page="maps/" %}

### totalcross.net 

It is in the package totalcross.net where the connection classes are. Are they:

* Socket FTP;
* HTTPStream;
* ServerSocket;
* mail \(pop3\);
* SSL

### totalcross.phone 

The classes responsible for handling telephones are:

* CellInfo 
* Dial 
* SMS

### totalcross.sys 

The totalcross.sys package contains the utility and usage classes for Virtual Machine. Are they:

* Convert 
* Setting 
* Time 
* VM

### totalcross.unit 

The classes responsible for building unit tests are in the totalcross.unit package. The classes are: 

* TestCase
* TestSuite
* UIRobot

### totalcross.util 

Utilities classes

* Date Hashtable / Vector
* IntHastable / IntVector 
* Random 
* Collections 
* concurrent.Lock 
* BigDecimal / BigInteger 
* PDFWritter 
* Regex 
* Zip/ZLib/GZip

### totalcross.xml

In the package totalcross.xml are the classes responsible for XML handling. They are:

* XMLRPC com Axis 
* SOAP
* XMLTokenizer

## References

* For a better understanding, see the [javadoc](http://rs.totalcross.com/doc/index.html)

