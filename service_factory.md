# Service Factory
The Attivio Service Factory allows SDK users to access a set of Attivio services, or create custom services, that run on a node process.
## Usage
The Service Factory can be accessed in a variety of ways using a ServiceFactoryFactory.  Below are some examples of how to gain access to the ContentStoreProvider
###### When running in an Attivio component:
``` 
ServiceFactory serviceFactory = ServiceFactoryFactory.get(https://attivio.github.io/sdk-5.5-javadoc/com/attivio/sdk/client);
serviceFactory.getService(ContentStoreProvider.class)
ContentStoreProvider storeProvider = serviceFactory.getService(ContentStoreProvider.class)
```
###### When running in a separate process (such as in an AttivioRunnable):
``` 
String projectName = "myProject";
String environment = "production";
String zookeeperConnectionString = "localhost:16980";
ServiceFactory serviceFactory = ServiceFactoryFactory.getRemote(projectName, environment, zookeeperConnectionString);
ContentStoreProvider storeProvider = serviceFactory.getService(ContentStoreProvider.class)
```
##### List of Attivio services accessible through the ServiceFactory
* [IngestClient](https://attivio.github.io/sdk-5.5-javadoc/com/attivio/sdk/client/IngestClient.html)
* [EventStoreApi](https://attivio.github.io/sdk-5.5-javadoc/com/attivio/sdk/client/EventStoreApi.html)
* [IngestionHistoryApi](https://attivio.github.io/sdk-5.5-javadoc/com/attivio/sdk/client/IngestionHistoryApi.html)
* [SearchClient](https://attivio.github.io/sdk-5.5-javadoc/com/attivio/sdk/client/SearchClient.html)
* [SignalTrackingApi](https://attivio.github.io/sdk-5.5-javadoc/com/attivio/sdk/client/SignalTrackingApi.html)
* [RelevancyModelApi](https://attivio.github.io/sdk-5.5-javadoc/com/attivio/sdk/client/RelevancyModelApi.html)
* [AuditWriterApi](https://attivio.github.io/sdk-5.5-javadoc/com/attivio/sdk/client/audit/AuditWriterApi.html)
* [AuditReaderApi](https://attivio.github.io/sdk-5.5-javadoc/com/attivio/sdk/client/audit/AuditReaderApi.html)
* [DocumentStoreApi](https://attivio.github.io/sdk-5.5-javadoc/com/attivio/sdk/client/DocumentStoreApi.html)
* [ConnectorHistoryApi](https://attivio.github.io/sdk-5.5-javadoc/com/attivio/sdk/client/ConnectorHistoryApi.html)
* [ContentStoreProvider](https://attivio.github.io/sdk-5.5-javadoc/com/attivio/sdk/api/ContentStoreProvider.html)
* [AutoCompleteApi](https://attivio.github.io/sdk-5.5-javadoc/com/attivio/sdk/client/AutoCompleteApi.html)
