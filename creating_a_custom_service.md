## Creating a Custom Service
To create a service that can be accessed through the ServiceFactory, there are a couple of things that need to be configured, below you will see this process using an example service HelloWorldApi:  
##### 1.) Create an interface that extends `ExposedApi` such as this:
```
package com.my.app

@JmxManageable
public interface HelloWorldApi extends ExposedApi {

  @JmxReadable
  public String getHelloWorldString();

  @JmxWritable
  public String getHelloWorldString();

  @JmxInvocable
  public void helloWorld();
  
}
```
If you would like your service to be accessible remotely it needs to support being used via jmx.  Attivio provides JMX interactivity to classes which use annotations seen above (used appropriately per method depending on desired type of interactivity)
##### 2.) Create an implementation of your service that you intend to be used at runtime:
```
package com.my.app

import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

public class HelloWorldApiImpl {

  private Logger log = LoggerFactory.getLogger(HelloWorldApiImpl.class);
  private String helloWorldString = "hello world";

  public String getHelloWorldString() {
    return helloWorldString;
  }

  public void setHelloWorldString(String helloWorldString) {
    this.helloWorldString = helloWorldString;
  }
  
  public void helloWorld() {
    log.info(helloWorldString());
  }
  
}
```
##### 3.) Register the implementation as a bean in the beans.xml file (located in the src/main/resources folder of the project)
```
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans" 
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:util="http://www.springframework.org/schema/util"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd
                           http://www.springframework.org/schema/util http://www.springframework.org/schema/util/spring-util.xsd">


  <bean name="sampleService" class="com.bborchard.attiviomodule.SampleAttivioServiceImpl" lazy-init="true"/> <!-- this is the service -->

</beans>

```
##### 4.) If desired, create a mock implementation of your service:
```
package com.my.app

import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

public class MockHelloWorldApi {

  private Logger log = LoggerFactory.getLogger(MockHelloWorldApi.class);
  private String helloWorldString = "hello from junit test";
  
  public String getHelloWorldString() {
    return helloWorldString;
  }

  public void setHelloWorldString(String helloWorldString) {
    this.helloWorldString = helloWorldString;
  }

  public void helloWorld() {
    log.info(helloWorldString());
  }
  
}
```
Mock implementations are used when testing.  They are not strictly necessary if the runtime implementation of a service works in a testing environment.
##### 5.) Register your mock in attivio.test.json 
```
{
  "testAssociations" : {
    "TestApi" : "com.my.app.MockHelloWorldApi"
  }
}
```
If no mock is created, the runtime implementation must be specified in this file so that the ServiceFactory knows what service implementation to use during testing
##### 6.) Access your service using the ServiceFactory  
```
HelloWorldApi helloWorldApi = ServiceFactoryFactory.get().getService(HelloWorldApi.class);
helloWorldApi.helloWorld();
```

The service should now work whether it is being used in the node process, remotely in a separate process (for example aie-exec), or in a junit test.  The implementation in the test association in the attivio.test.json file will run during testing.