## Creating a Custom Service
To create a service that can be accessed through the ServiceFactory, there are a couple of things that need to be configured, below you will see this process using an example service HelloWorldApi:  
1.) Create an interface that is annotate with the annotation `ExposedApi`, this will be the service:
```
package com.my.app

@ExposedApi
public interface HelloWorldApi {

  public void helloWorld();
  
}
```
2.) Create an implementation of your service that you intend to be used at runtime:
```
package com.my.app

import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

public class HelloWorldApiImpl {

  private Logger log = LoggerFactory.getLogger(HelloWorldApiImpl.class);
  public String helloWorldString = "hello world";
  
  public void helloWorld() {
    log.info(helloWorldString);
  }
  
}
```
3.) Register an implementation as a bean in the attivio.module.json file  
4.) If you wish, create a mock implementation of your service:
```
package com.my.app

import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

public class MockHelloWorldApi {

  private Logger log = LoggerFactory.getLogger(MockHelloWorldApi.class);
  
  public void helloWorld() {
    log.info("hello from junit test");
  }
  
}
```
5.) Register your mock in attivio.test.json (note that if no mock is created, the runtime implementation must be specified in this file so that the MockServiceFactory knows what service implementation to use)
```
{
  "testAssociations" : {
    "TestApi" : "com.my.app.MockHelloWorldApi"
  }
}
```
6.) Access your service using the ServiceFactory  
```
HelloWorldApi helloWorldApi = ServiceFactoryFactory.get().getService(HelloWorldApi.class);
helloWorldApi.helloWorld();
```