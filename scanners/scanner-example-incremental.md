# Incremental Scanner Example

The sample Attivio project contains the `com.sample.module.SampleIncrementalDataSourceScanner` sample scanner. As in the `com.sample.module.SampleDataSourceScanner` sample scanner, the scanner can be tested standalone from the `SampleIncrementalDataSourceScannerTest` Junit test and from the connectors admin page.

The incremental sample scanner demonstrates the following SDK capabilities.

| Capability | Notes |
| :--- | :--- |
| Feeding only new and modified documents: | Observe the `shouldFeedThisDoc` method `IngestionHistoryApi` calls. |
| Deleting obsolete documents | Observe the `deleteObsoleteDocuments` method. |
| Securing the documents | Observe the `createACL` method. |
| Creating document meta data in addition to content | Observe the `addMetadata` method. |
| Storing content in the content store | Observe the calling to the `DocumentPublisher.put` method. |
| Committing documents in the index explicitly by the scanner | Observe the `IndexCommitter.commit` call. |
| Using annotations to create menus | Observe the `@ConfigurationOptionInfo.Group` annotations. |
| Using annotations to display and describe the scanner | Observe the `@ConfigurationOptionInfo` annotation. |
| Using annotations to display and describe each option | Observe the `@ConfigurationOption` annotation with the `displayName`, `description` and `formEntryClass` arguments. |

