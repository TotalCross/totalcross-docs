# SOAP

## Overview

> “SOAP Version 1.2 \(SOAP\) is a lightweight protocol intended for exchanging structured information in a decentralized, distributed environment. It uses XML technologies to define an extensible messaging framework providing a message construct that can be exchanged over a variety of underlying protocols. The framework has been designed to be independent of any particular programming model and other implementation specific semantics.” - Definition from SOAP Version 1.2 Part 1: Messaging Framework \(Second Edition\) - W3C Recommendation 27 April 2007

Because of its implementation independence, the SOAP protocol is widely used on the implementation of Web Services.

## The SOAP Class

This class represents a SOAP message that, when executed, is sent to the server in a HTTP request. The server response is then received, processed, and the answer made available.

Before creating a instance of **SOAP**, you may set the following class fields:

* The prefix string used to start the request. Note that it uses UTF-8, so unicode characters are not supported. Its default value is:

```markup
<?xml version="1.0" encoding="UTF-8"?>
<soapenv:Envelope xmlns:soapenv="
http://schemas.xmlsoap.org/soap/envelope/"
xmlns:xsd="http://www.w3.org/2001/XMLSchema"
xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
<soapenv:Body>
```

* suffix The suffix string used to finish the request. Its default value is:

```markup
</soapenv:Body>
</soapenv:Envelope>
```

debug Changing this value to true enables debug mode, which writes XML parsing information on the debug console \(or the default error output when running on JDK\). You may also set HttpStream.debugHeader = true.  
Caution: don’t use this on device because it increases a lot the memory usage.

disableEncoding The SOAP request will ask the server for GZip or ZLib encoded response by default. To disable encoding, **set this field to true**.

## Constructors

 To create a new **SOAP** instance, you must use the following constructor:

| Type | Name | Description |
| :--- | :--- | :--- |
| **constructor** | SOAP\(String mtd, String uri\) | Creates a new SOAP request where mtd specifies the remote method to be executed, and uri, the address of the Web Service. The default namespace will be used, along with an open timeout of 25 seconds, and a read and write timeout of 60 seconds. |

## Instance Fields

After creating a new **SOAP** object, you may set some of its following instance fields:

| Type | Name | Description |
| :--- | :--- | :--- |
| **boolean** | wasCompressionUsed | A flag that indicates if the SOAP connection was using either GZip or ZLib. This is a ready-only flag, set during the execute\(\) method, and changing its value has no effect. |
| **String** | alternativeReturnTag | By default, the XML parser used by SOAP will recognize as an answer tag any tags whose name ends with “result” or “return” \(ignoring the case\). This field, if set, specifies an alternative answer tag name, recognizing any XML element that ends with the specified value as an answer tag. AlternativeReturnTag IS CASE SENSITIVE, unlike the SOAP default tag names. Also, alternativeReturnTag does not replace the default values. It’s just a new value with higher priority over the default ones. |
| **String** | namespace | String that identifies the service’s namespace. Its default value is: http://schemas.xmlsoap.org/soap/. |
| **int** | openTimtout | Specifies the connection open timeout value in milliseconds. Its default value is defined by the constant DEFAULT\_OPEN\_TIMEOUT \(25 s\). |
| **int** | readTimeout | Specifies the connection read timeout value in milliseconds. Its default value is defined by the constant DEFAULT\_READ\_TIMEOUT \(60 s\). |
| **int** | writeTimeout | Specifies the connection write timeout value in milliseconds. Its default value is defined by the constant DEFAULT\_WRITE\_TIMEOUT \(60 s\). |
| **String** | mtd | Stores the name of the remote method. |
| **String** | uri | Stores the address to the Web Service. |

You may change both the **mtd** and the **uri** values before executing the request. Although this seems to be pointless, because these values are passed to the constructor.

If the remote method expects any arguments, you must set them using the **`setParam()`** method. However, there are several versions of this method to cover different argument types. Listing all of them would be pointless, so we’ll define a generic type that we’ll refer as , and may be one of the of the following:

* int 
* boolean 
* double 
* String 

So, whenever a SOAP method is described like **`setParam( param)`**, you can safely assume there are four versions of this method, one for each type listed above. Other type of parameters can be passed using similar methods. Unicode characters are not accepted because the default header uses UTF-8.

## SOAP methods for parameters setting:

| Type | Name | Description |
| :--- | :--- | :--- |
| **void** | setParam\( param\) | Sets the given value in the method’s argument order. |
| **void** | setParam\(\[\] param\) | Sets the given array in the method’s argument order. |
| **void** | setParam\( param, String paramName\) | Sets the given value, identifying it with the given parameter name. |
| **void** | setParam\(\[\] param, String paramName\) | Sets the given array value, identifying it with the given parameter name. |
| **void** | setParam\(byte\[\] param, String paramName\) | Sets a byte array value, identifying it with the given parameter name. |
| **void** | setParam\(String param, String paramName, String paramType\) | Sets a String parameter in the method, identifying it with the given name and specifying its type as the given one. |
| **void** | setParam\(String\[\] param, String paramName, String paramType\) | Sets a String array value, identifying it with the given parameter name and specifying its type as the given one. |
| **void** | setObjectParam\(String paramName,String\[\] fieldNames, String\[\] fieldValues\) | Sets an Object parameter value, by specifying its parameter name, field names and field values. |
| **void** | setObjectArrayParam\(String paramName,String\[\] fieldNames, Vector fieldValues\) | Sets an Object array parameter value, by specifying its parameter name, field names and field values. |

The only thing left to do now is to execute the request and check the service’s answer:

| Type | Name | Description |
| :--- | :--- | :--- |
| **void** | execute\( \) | This method simply executes the prepared SOAP request. |
| **Object** | getAnswer\( \) | To retrieve the method’s answer, you must call this method after execute\(\). The return type of this method is Object, but it may return only three different values \(the values may be escaped; use totalcross.ui.html.EscapeHtml.unescape\(\) to convert it back\). The remote method return type is known, so you may just typecast the Object returned by getAnswer\(\) to String or String array, converting its values if necessary. The possible returns are: 1- null When the remote method has no return value or the execution failed for any reason. 2- String When the remote method returns a single value. If the expected value is not String, you must convert the received String to the right type \(e.g. if you’re expecting an int value, you can use Convert.toInt\(\)\). 3- String\[\] When the remote method returns an array or an Object. If the expected value is not a String array, you must convert each value of the array to the right type. If it’s an object, the array contains its field values. |
| **void** | useProxy\(String address, int port, String username, String password\) | Sets the proxy settings to be used by the SOAP connection. You may optionally set the username and password for basic proxy authorization. Proxy authorization is disabled if either username or password is null. In this method, address is the proxy address port and port is the proxy port. |

## References

* For more details, check out the **totalcross.xml.soap** package [JavaDocs](https://rs.totalcross.com/doc/).

