# SQLite Encryption

## Overview

Allows reading and writing encrypted database files. All database content, including the metadata, is encrypted so that to an outside observer the database appears to be white noise.

The following encryption algorithms are currently supported:

* AES-128 in OFB mode \(default\)
* AES-256 in OFB mode

## **Key Formats**

There are three different key formats. The first format

```java
props.put("key", new Properties.Str("'secret-password'"));
```

takes the key string and repeats it over and over until it exceeds the number of bytes in the key of the underlying algorithm \(16 bytes for AES128, 32 bytes for AES256, or 256 bytes for RC4\). It then truncates the result to the algorithm key size. The approach limits the key space since it does not allow 0x00 bytes in the key. The second format

```java
props.put("hexkey", new Properties.Str("'secret-password'"));
```

accepts the key as hexadecimal, so any key can be represented. If the provided key is too long it is truncated. If the provided key is too shorted, it is repeated to fill it out to the algorithm key length. The third format

```java
props.put("textkey", new Properties.Str("'secret-password'"));
```

computes a strong hash on the input key material and uses that hash to key the algorithm. The -textkey format is recommended for new applications.

## **Key Material**

The amount of key material actually used by the encryption extension depends on the algorithm. With see-rc4.c, the first 256 byte of key are used. With aes-128, the first 16 bytes of the key are used. With aes-256, the first 32 bytes of key are used.

If you specify a key that is shorter than the maximum key length, then the key material is repeated as many times as necessary to complete the key. If you specify a key that is larger than the maximum key length, then the excess key material is silently ignored. For the

```java
props.put("textkey", new Properties.Str("'secret-password'"));
```

option, up to 256 bytes of the passphrase are hashed using RC4 and the hash value becomes the encryption key. Note that in this context the RC4 algorithm is being used as a hash function, not as a cryptographic function, so the fact that RC4 is a cryptographically weak algorithm is irrelevant.

## **Encryption algorithm selection using a key prefix**

The key may begin with a prefix to specify which algorithm to use. The prefix must be exactly one of "aes128:", or "aes256:". The prefix is not used as part of the key sent into the encryption algorithm. So the real key should begin on the first byte after the prefix. Take note of the following important details:

* The prefix is case sensitive. "aes256:" is a valid prefix but "AES256:" is not.
* If the key prefix is omitted or misspelled, then the encryption algorithm defaults to "aes128" and the misspelled prefix becomes part of the key.
* The algorithm prefix strings work on the "see.c" variant of SEE only. For any of see-aes128-ofb.c, see-aes255-ofb.c or see-aes128-ccm.c any prefix on the key is interpreted as part of the key.
* When using PRAGMA hexkey or PRAGMA hexrekey, the key prefix must be hex encoded just like the rest of the key.

```java
props.put("hexkey", new Properties.Str("'aes128:6d796b6579'"));          // Wrong!!
props.put("hexkey", new Properties.Str("'6165733132383a6d796b6579'"));   // correct
```

### **Limitations**

* TEMP tables are not encrypted.
* In-memory \(":memory:"\) databases are not encrypted.
* Bytes 16 through 23 of the database file contain header information which is not encrypted.
* Encryption is **NOT** supported on the simulator. To be able to use it, you need to remove the encryption. That can be done with a native Totalcross application like the previous example sending a empty value to rekey
* Only supported for Pro or Enterprise users; Applications using old or free keys can´t use encryption.

## **Usage**

In the following code, you can see a basic usage of SQLite Encryption example. You just need to instance a Properties, put a "key" property and set the key as the value. Then, you just need to open a new connection passing the properties as an argument.

Instead of the **key**, you can also pass **hexkey** or **textkey** as the key argument.

```java
Properties props = new Properties();
props.put("key", new Properties.Str("'secret-password'"));
Connection con = DriverManager.getConnection("jdbc:sqlite:" + Convert.appendPath(Settings.appPath, "database.db"), props);
```

{% hint style="warning" %}
**Attention**: the key must be between **single quotes**.
{% endhint %}

### **Changing the encryption key**

There also exists the **rekey** property\(and, equivalently, hexrekey and textrekey\) which can be used to change the database encryption key. Usage example:

```java
Properties props = new Properties();
props.put("key", new Properties.Str("'secret-password'"));
props.put("rekey", new Properties.Str("'new-password'"));
Connection con = DriverManager.getConnection("jdbc:sqlite:" + Convert.appendPath(Settings.appPath, "database.db"), props);
```

### **Removing the encryption key**

To remove the encryption from the bank and save it on the original format, you just have to use rekey and set a empty value: \(but obviously, you need the original key\)

```java
Properties props = new Properties();
props.put("key", new Properties.Str("'secret-password'"));
props.put("rekey", new Properties.Str("''"));
Connection con = DriverManager.getConnection("jdbc:sqlite:" + Convert.appendPath(Settings.appPath, "database.db"), props);
```

