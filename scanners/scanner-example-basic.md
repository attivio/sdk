# Basic Custom Scanner Example

The sample Attivio project contains the `com.sample.module.SampleDataSourceScanner` sample scanner. There are two ways to run the sample scanner:

* As a standalone test: Run the `SampleDataSourceScannerTest` Junit test.
* From the connectors administration page: Go to the connectors administration page after the sample Attivio project was created and Attivio was started. Create a new "Simple Sample Scanner" connector and start it.

Examine how the following phases of the scanner life-cycle are implemented below.

## Configuring the scanner

* Observe the `@ConfigurationOptionInfo` annotation that describes the scanner in the UI administration page and specifies its preferred workflow.
* Observe the `setTestText` and `getTestText` configuration methods.
* Observe the `@ConfigurationOptionInfo` `@ConfigurationOption` annotation that tells the UI how to present and how to process the configuration options.

## Validating the configuration

* Observe the `validateConfiguration` optional method that throws an exception if `testText` was not configured

## Creating documents and feeding the workflow

* Observe the start method:  
  * It creates a document with the "1" document id.
  * It loads the document with the configured text.
  * It feeds the document through the publisher.

