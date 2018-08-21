# Writing and Testing Scanners

Attivio supports the implementation of custom scanners to deliver content into the Attivio workflow from any data source. The SDK specifies the interfaces and annotations the scanner should implement so that
it can be configured and controlled from the administration UI. The SDK also specifies the interfaces exposed by Attivio the scanner can use to feed content and access Attivio services.

## A Basic Custom Scanner Example

The sample Attivio project contains the `com.sample.module.SampleDataSourceScanner` sample scanner. There are two ways to run the sample scanner:
- As a standalone test: Run the `SampleDataSourceScannerTest` Junit test.
- From the connectors administration page: Go to the connectors administration page after the sample Attivio project was created and Attivio was started. Create a new "Simple Sample Scanner" connector and start it.

Examine how the following phases of the scanner life-cycle are implemented:

##### Configuring the scanner
- Observe the @ConfigurationOptionInfo annotation that describes the scanner in the UI administration page and specifies its preferred workflow.
- Observe the setTestText and getTestText configuration methods.
- Observe the @ConfigurationOptionInfo @ConfigurationOption annotation that tells the UI how to present and how to process the configuration options.

##### Validating the configuration
- Observe the validateConfiguration optional method that throws an exception if testText was not configured

##### Creating documents and feeding the workflow
- Observe the start method:  
	It creates a document with the "1" document id.  
	It loads the document with the configured text.  
	It feeds the document through the publisher.  


## The Incremental Scanner Example

The sample Attivio project contains the `com.sample.module.SampleIncrementalDataSourceScanner` sample scanner. As in the `com.sample.module.SampleDataSourceScanner` sample scanner,
the scanner can be tested standalone from the `SampleIncrementalDataSourceScannerTest` Junit test and from the connectors admin page. The incremental sample scanner demonstrates the following SDK capabilities:
- **Feeding only new and modified documents:** Observe the shouldFeedThisDoc method IngestionHistoryApi calls.
- **Deleting obsolete documents:** Observe the deleteObsoleteDocuments method.
- **Securing the documents:** Observe the createACL method.
- **Creating document meta data in addition to content:** Observe the addMetadata method.
- **Storing content in the content store:** Observe the calling to the DocumentPublisher.put method.
- **Committing documents in the index explicitly by the scanner:** Observe the IndexCommitter.commit call.
- **Using annotations to create menus:** Observe the @ConfigurationOptionInfo.Group annotations.
- **Using annotations to display and describe the scanner:** Observe the @ConfigurationOptionInfo annotation.
- **Using annotations to display and describe each option:** Observe the @ConfigurationOption annotation with the displayName, description and formEntryClass arguments.


## The Principal Scanner Example

The sample Attivio project contains the `com.sample.module.SamplePrincipalScanner` sample scanner. The sample shows how to create Attvio users and groups.
Attivio distributes and documents the Active Directory Principal Scanner and the Ldap Principal Scanner. These scanners cover the majority of use cases. But sometimes it is required
to create Attivio users and groups from other sources. The sample demonstrates the following:  
- The creation of AttivioPrincipal objects (users and groups).
- Using AttivioGroupMembership to add members to groups.
- Using the DocumentPublisher.feed method to create principals in the Attivio index.


## Glossary

This is a gloassary of the main interfaces and classes relevant to scanner implementation:  

 - **com.attivio.sdk.scanner.DataSourceScanner:** The interface every scanner must implement.  
 - **com.attivio.sdk.connector.DocumentPublisher:** The interface used by the scanner to create and delete documents and principals.  
 - **com.attivio.sdk.ingest.IngestDocument:** The document create by the scanner and fed through the DocumentPublisher.  
 - **com.attivio.sdk.schema.FieldNames:** The names of standard Attivo fields. These fields are already defined in the schema.  
 - **com.attivio.sdk.client.IngestionHistoryApi:** Service that allow the scanner to persist and retrieve the scanner state across runs.  
 - **com.attivio.sdk.scanner.IncrementalDataSourceScanner:** The scanner should implement this interface when incremental scan is required.  
 - **com.attivio.sdk.security.*:** Model classes to create principals and ACLs in order to control who is allowed to read Attivio documents.  
 - **com.attivio.sdk.server.annotation.*:** Use annotations define the administration UI for scanners and other Attivio components.  

