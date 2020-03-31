# API Rest

### Verbs

HTTP verbs are the request methods we use along with the endpoints to access a particular api route.

| Endpoint | Verbs | Action |
| :--- | :--- | :--- |
| /get | GET | Retrieves new information |
| /post | POST | Create new information |
| /put | PUT | Change an information |
| /delete | DELETE | Delete information |

### Requisitions

One of the ways to make requests is to create **PressListener** for Button, in the example below I will demonstrate how to get the response of the request in a variable and display in a Label

{% code title="PressListener" %}
```java
//String uri = Requisition URL
//HttpMethod httpMethod = HTTP Verbs
    PressListener getPressListener(final String url, String httpType) {
        return (e) -> {
            //msg variable will be responsible for storing the request response
            String msg = "";

            try {

                HttpStream.Options options = new HttpStream.Options();
                options.httpType = httpType;

                HttpStream httpStream = new HttpStream(new URI(url), options);
                ByteArrayStream bas = new ByteArrayStream(4096);
                bas.readFully(httpStream, 10, 2048);
                String data = new String(bas.getBuffer(), 0, bas.available());

                Response<ResponseData> response = new Response<>();
                response.responseCode = httpStream.responseCode;
                
                if (httpStream.responseCode == 200){
                        response.data = (JSONFactory.parse(data, ResponseData.class));
                        
                        //Accessing the answer and picking up the information.
                        msg += "Url: " + response.data.getUrl() + "\n";
                        msg += "Origin: " + response.data.getOrigin();
                }
            } catch (IOException e1) {
                    msg = "erro";
            } catch (InstantiationException ex) {
                ex.printStackTrace();
            } catch (InvocationTargetException ex) {
                ex.printStackTrace();
            } catch (NoSuchMethodException ex) {
                ex.printStackTrace();
            } catch (IllegalAccessException ex) {
                ex.printStackTrace();
            }

            lblResult.setText(msg);
            lblResult.setRect(KEEP, KEEP, PREFERRED, PREFERRED);

        };
    }
    
    public static class Response<T> {
        public T data;
        public int responseCode;
    }

```
{% endcode %}

Creating the packet to receive the response in order to handle the data obtained from the request

{% code title="Structures" %}
```text
└── src
    └── main
        └── java
            └── com.your_company_name.your_name_app
                .
                .
                .
                └── ResponseData
                    └── Args
                    └── ResponseData
```
{% endcode %}

and now create the class to store the information

{% tabs %}
{% tab title="ResponseData class" %}
```java
package com.totalcross.RestApi.ResponseData;

public class ResponseData {

    Args args;
    String origin;
    String url;

    public Args getArgs() {
        return args;
    }

    public void setArgs(Args args) {
        this.args = args;
    }

    public String getOrigin() {
        return origin;
    }

    public void setOrigin(String origin) {
        this.origin = origin;
    }

    public String getUrl() {
        return url;
    }

    public void setUrl(String url) {
        this.url = url;
    }
}


```
{% endtab %}

{% tab title="Args class" %}
```java
package com.totalcross.RestApi.ResponseData;

public class Args {

    private String args;

    public String getArgs() {
        return args;
    }

    public void setArgs(String args) {
        this.args = args;
    }

}


```
{% endtab %}
{% endtabs %}

Now just put that pressListener on your button by changing only the endpoint and the verb, see the example below

```java
@Override
    public void initUI() {
        String binUrl = "http://httpbin.org";

        Button btnGet = new Button("GET");
        btnGet.addPressListener(getPressListener(binUrl + "/get", HttpStream.GET));
        add(btnGet, LEFT, AFTER, FILL, fmH * 3);

        Button btnPost = new Button("POST");
        btnPost.addPressListener(getPressListener(binUrl + "/post", HttpStream.POST));
        add(btnPost, LEFT, AFTER, FILL, fmH * 3);

        Button btnPut = new Button("PUT");
        btnPut.addPressListener(getPressListener(binUrl + "/put", HttpStream.PUT));
        add(btnPut, LEFT, AFTER, FILL, fmH * 3);

        Button btnDelete = new Button("DELETE");
        btnDelete.addPressListener(getPressListener(binUrl + "/delete", HttpStream.DELETE));
        add(btnDelete, LEFT, AFTER, FILL, fmH * 3);


        lblResult = new Label(" ");
        add(lblResult, LEFT, AFTER);
    }
```

### References 

* See the complete API code remainder with TotalCross in [GitHub](https://github.com/TotalCross/ApiSample).

