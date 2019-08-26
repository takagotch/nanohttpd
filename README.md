### nanohttpd
---
https://github.com/NanoHttpd/nanohttpd

```java
server.makeSecure(NanoHTTPD.makeSSLSocketFactory("/keystore.jks", "password".toCharArray()), null);

package com.example;

import java.io.IOException;
import java.util.Map;

import fi.iki.elonen.NanoHTTPD;

public class App extends NanoHTTPD {
  
  public App() throws IOException {
    super(8080);
    start(NanoHTTPD.SOCKET_READ_TIMEOUT, false);
    System.out.println("\nRunning! Point your browsers to https://localhost:8080/ \n");
  }
  
  public static void main(String[] args) {
    try {
      new App();
    } catch (IOException ioe) {
      System.err.println("Couuldn't start sever:\n" + ioe);
    }
  }
  
  @Override
  public Response serve(IHTTPSession session) {
    String msg = "";
    Map<> parms = session.getParms();
    if (parms.get() == null) {
      msg += "<form action='?' method='get'>\n <p>Your name: <input type='text' name='username'></p>\n" + "</form>\n";
    } else {
      msg += "<p>Hello, " + parms.get("username") + "!</p>"
    }
    return newFixedLengthResponse(msg + "</body></html>\n");
  }
}
```

```sh
mvn compile
mvn exec:java -pl webserver -Dexec.mainClass="org.nanohttpd.webserver.SimpleWebServer"
mvn archetype:generate -DgroupId=com.example -DartifactId=myHelloApp -DinteractiveMode=false
mvn compile
mvn exec:java-Dexec.mainClass="com.example.App"
```

```
```


