Cloudopt-plugin-encrypt is a Cloudopt Next encryption toolkit. Currently supports Base64, MD5, AES, RSA, DES, Sha1, and Sha encryption algorithms.

Please refer to the appropriate dependencies before use. If you do not inherit cloudopt-next-parent, please add the version number yourself.

````xml
<dependency>
    <groupId>net.cloudopt.next</groupId>
    <artifactId>cloudopt-next-encrypt</artifactId>
</dependency>
````

## Base64

````kotlin
var e = Base64Encrypt()
var s = e.encrypt("hello")
println(s)
println(e.decrypt(s))
````

````java
Encrypt e = new Base64Encrypt();
String s = e.encrypt("hello");
System.out.println(s);
System.out.println(e.decrypt(s));
````

## MD5

````kotlin
var e = MD5Encrypt()
var s = e.encrypt("hello")
println(s)
````

````java
Encrypt e = new MD5Encrypt();
String s = e.encrypt("hello");
System.out.println(s);
````

## AES

````kotlin
var e = AesEncrypt()
var s = e.setPassword("lKY7YO6jqRnzNOJ3").encrypt("hello")
println(s)
println(e.decrypt(s))
````

````java
Encrypt e = new AesEncrypt();
String s = e.setPassword("lKY7YO6jqRnzNOJ3").encrypt("hello");
System.out.println(s);
System.out.println(e.decrypt(s));
````

## RSA

````kotlin
var publicK = "MIGfMA0GCSqGSIb3DQEBAQUAA4GNADCBiQKBgQCFmf/HWpTZ9smPjyM6SUa0UvUQGfIY+OMV5S8zNqmwz11pYovtz57okRZreK8RtBkBOcOKyk7KRMm0agMm0qBaz0ESuFJmIbl3pEn3l/m0aCNnFv2ehijXl6AoW3bB/fKFoKUcRGXet4R/ka1qcxUJaH3uZtmiyPn8G66BhZXBbQIDAQAB"
var privateK = "MIICdgIBADANBgkqhkiG9w0BAQEFAASCAmAwggJcAgEAAoGBAIWZ/8dalNn2yY+PIzpJRrRS9RAZ8hj44xXlLzM2qbDPXWlii+3PnuiRFmt4rxG0GQE5w4rKTspEybRqAybSoFrPQRK4UmYhuXekSfeX+bRoI2cW/Z6GKNeXoChbdsH98oWgpRxEZd63hH+RrWpzFQlofe5m2aLI+fwbroGFlcFtAgMBAAECgYAZMloS9vprwSdyc8RpEbjL+XlOeBY4r3fkgTzNo9mNBw7O+U76otWNdw+LZU9fP2AX4xUF7/G8JA0GgZfmkoK7VTbpBpX7BeW664GzVa9sDFsf2WMD01J9mndcHjcyyeuwBSXliJupjDAxpDTWcd6U2gMgv0SsTxCZQo2Wdr0y4QJBAPP/OY4Mc68P2bwBXyJcnKZYC0sSgeudZ8URXNbNtEgiklO5SV5hteEBfHYjCzbLf7zE38pMNVtuNua2paNM1kcCQQCMLIKO3wRDQgo/LZxy58kjknAVbZJypZj6Yz8O8poIB2sUyyBPNVOXLg4eOSBMQXH2yJNIw4kv+KAxA+8D2GCrAkEAwHV7Ao7T2SxZhLBYSBRhA9zC2653iFAagBlX759GKvgKD7xBIQ9VlWvErrKpr8kIsu9fzoQaOkpPR+Cd+pcrFQJAfrfmNx5pjhvvg3nKSx46+UtyxAxQLhCCISkDYpHyqXt7VErlJHYC4VKjNLNT/VvUmNJuQ4NxS8qplmYF9yXvDQJAO/GlhZ+qmCOpfKb/pOHRUYSZsPZ0/85sQDQ2u/GYp4jtDqeYNoqZt0Oqr9bEJkJ2sRZnoRGXUePuR7kMoejy9w=="
var e = RsaEncrypt()
e.setPublicKey(publicK).setPrivateKey(privateK)
var s = e.encrypt("hello")
println(s)
println(e.decrypt(s))
````

````java
Encrypt e = new RsaEncrypt();
e.setPublicKey(publicK).setPrivateKey(privateK);
String s = e.encrypt("hello");
System.out.println(s);
System.out.println(e.decrypt(s));
````

## DES

````kotlin
var e = DesEncrypt().setPassword("12345678")
var s = e.encrypt("hello")
println(s)
println(e.decrypt(s))
````

````java
Encrypt e = new DesEncrypt().setPassword("12345678");
String s = e.encrypt("hello");
System.out.println(s);
System.out.println(e.decrypt(s));
````

## Sha1

````kotlin
var e = SHA1Encrypt()
var s = e.encrypt("hello")
println(s)
````

````java
Encrypt e = new SHA1Encrypt();
String s = e.encrypt("hello");
System.out.println(s);
````

## Sha

````kotlin
var e = SHAEncrypt()
var s = e.encrypt("hello")
println(s)
````

````java
Encrypt e = new SHAEncrypt();
String s = e.encrypt("hello");
System.out.println(s);
````