# JSON

## Overview

Json is a way to structure data quickly and with good readability and has a key/data structure very similar to the java hasmap or the python dictionary.

## How to use

the two ways to use JSON in TotalCross:

### Beans

You need to create the data beans that will be received in JSON

```java
//Where the data parameter is a variable that contains the JSON
Response response = JSONFactory.parse(data, Response.class);
```

You can see more abount this in [REST API](https://app.gitbook.com/@totalcross/s/playbook/apis/api-rest)

### JSON Object

```java
//Where the data parameter is a variable that contains the JSON
JSONObject jsonObject = new JSONObject(data);
```

You can use the variable jsonObject  like a hashmap.

## Referencies

* See a project on github using[ JSON](https://github.com/TotalCross/ApiSample)



