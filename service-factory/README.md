# Service Factory

## Usage

The Service Factory can be accessed in a variety of ways using a `ServiceFactoryFactory`. Below are some examples of how to gain access to the `ContentStoreProvider`

### When running in an Attivio component:

```java
ServiceFactory serviceFactory = ServiceFactoryFactory.get();
serviceFactory.getService(ContentStoreProvider.class)
ContentStoreProvider storeProvider = serviceFactory.getService(ContentStoreProvider.class)
```

### When running in a separate process \(such as in an `AttivioRunnable`\):

```java
String projectName = "myProject";
String environment = "production";
String zookeeperConnectionString = "localhost:16980";
ServiceFactory serviceFactory = ServiceFactoryFactory.getRemote(projectName, environment, zookeeperConnectionString);
ContentStoreProvider storeProvider = serviceFactory.getService(ContentStoreProvider.class)
```

## List of Attivio services accessible through the Service Factory

* `IngestClient`
* `EventStoreApi`
* `IngestionHistoryApi`
* `SearchClient`
* `SignalTrackingApi`
* `RelevancyModelApi`
* `AuditWriterApi`
* `AuditReaderApi`
* `DocumentStoreApi`
* `ConnectorHistoryApi`
* `ContentStoreProvider`
* `AutoCompleteApi`

