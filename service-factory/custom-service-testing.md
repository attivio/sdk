# Testing with the ServiceFactory

Any functionality that makes use of the `ServiceFactory` whether in Attivio SDK or in a custom written piece of functionality, will behave differently when run in a testing environment.

## Differentiation Between Test and Runtime

In the Attivio SDK, whether or not a process is running as a test is determined by the inclusion of the testutils jar on the classpath. This jar is not part of the install, but is included by default in the Attivio SDK archetype as a test dependency. Specifically, Attivio checks for the presence of the attivio.test.json file on the classpath. This is included \(and empty\) in the testutils jar, but will be overwritten by the version of that file in the archetype.

At runtime Attivio will find an implementation of the service from a bean, whereas in a test Attivio will find an implementation \(beyond what is default\) from the attivio.test.json file using the testAssociations field. To learn more about how this works in the context of a custom service, see [Creating a Custom Service](custom-service-creating.md).

## Mock Services

Attivio provides mock services for all service implementations available through the `ServiceFactory`. These mock services can be anything from lightweight versions of the runtime services to noop services that allow for method invocation but provide no actual functionality. Some of these mock services require information to be registered with them at the beginning of a test in order to do anything. One such example is the `MockSearchClient`, for which there is a usage example in the file `SampleAttivioRunnableTest.java` in the archetype.

Custom mock services can be written as needed for specific projects and will override the defaults if they are registered in the testAssociations field in the `attivio.test.json` file in a project.

## Cleanup

Mock services will sometimes have in memory fields used to cache data that is handled at runtime by a more complicated data storage mechanism. For all provided mocks, any such caches are effectively cleared when a new instance of the mock object is created. The nature of the `ServiceFactory` is such that instances of mock services \(and therefore mock data\) will persist through all tests run in a single process. This is generally not the desired behavior when testing and to avoid this, the `SdkRule` in the Attivio SDK can be declared, instantiated, and properly annotated in order to have all references to existing mock services cleared so they are reinstantiated when they are next fetched by the `ServiceFactory`. To learn more about Junit Rules, see [this page](https://junit.org/junit4/javadoc/4.12/org/junit/Rule.html)

