# IMEI in Android 10

> "**IMEI** is short for International Mobile Equipment Identity and is a unique **number** given to every single mobile phone, typically found behind the battery. **IMEI numbers** of cellular phones connected to a GSM network are stored in a database \(EIR - Equipment Identity Register\) containing all valid mobile phone equipment."

As of Android 10 \(API Level 29\) Google has dropped support to `getImei()`. This decision was taken because of their privacy policy, on this API Level, third parties - us - can't use it anymore. Thus, from the TotalCross ethical point of view,   we can't provide access to this information through our Android VM's anymore. Despite this can cause some issues with the way some TotalCross applications uses IMEI to identify end users, these same users can feel more secure, knowing his privacy is kept safe. You can find more info here: [https://developer.android.com/about/versions/10/privacy/changes\#randomized-mac-addresses](https://developer.android.com/about/versions/10/privacy/changes#randomized-mac-addresses).

Thus, in the next session we are going to show some alternatives to the IMEI in regarding to deal with the problem of identifying end users. 

## How are people going around this?

#### Random ID generator

This one is pretty simple, but also not so effective, you just need to generate a random number and check with your database if there's no other device with that ID, then you just set the new device ID as the random number. This solution is easy to implement but it requires a backend solution.

#### Mobile Device Management

For this you normally need a software solution that has management features for private mobile device vendors and as of yet, TotalCross does not support the MDM implementation. If you believe that it is necessary to implement this feature, please [contact us](mailto:vaneska.sousa@totalcross.com).

### What we recommed: Token based authentication

Whenever a new user tries to use your application, you should generate a token for that device, this will allow you to see who's using your application at any given moment, for this you should implement an authentication service on your backend, this service should return a token String if the login is successful. For the storage of the token we recommend you use [SQLite](https://learn.totalcross.com/learn-totalcross/how-to-store-data-sqlite).

#### How to use it in TotalCross

Get the token from server, then store it on the device.

```java
public boolean doLogin(username, password) {
    String tokenValue = doLogin(username, password);
    String sqliteRequest = "insert into userSettings values(?, ?)";
    PreparedStatement ps = dbConnection.prepareStatement(sqliteRequest);
    ps.setString(1, "token");
    ps.setString(2, tokenValue);
    ps.executeUpdate();
    ps.close();
    User user = getUserResources(tokenValue);
    if(tokenValue != null) {
        return true;
    } else {
        return false; // Wrong credentials, invalid login or password
    }
}
```

Get the token from device and get the user info.

```java
public boolean doLoginFromStoredToken() {
    Statement st = deConnection.createStatement();
    ResultSet rs = st.executeQuery("select * from userSettings");
    String token;
    if(rs.next()) {
        token = rs.getString("token");
        User user = getUserResources(token);
        return true;
    } else {
        return false; //Swap to login screen
    }
}
```



