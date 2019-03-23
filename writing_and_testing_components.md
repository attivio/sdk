# Writing and Testing Components

Attivio makes it easy to create custom components or stages for document, query, and response (to queries) processing.  The [README](https://github.com/attivio/sdk/blob/5.2/README.md) page provides instructions for using maven archetypes to generate examples.  This guide describes the interfaces and general processing architecture for Attivio components.  Components are small chunks of Java code which are executed by the Attivio framework as documents and queries pass through the system.  A good component should be focused on a small task (such as capitalizing text), keep little to no state, and be designed to be independent of other components in the system.  These principles make components reusable in other contexts and composable.

Your component may be created many times (multiple instances) within the same Java process.  This is used for parallelization purposes and to allow dynamic changes to take place.  For this reason, static data, expensive startup/shutdown code, and heavy memory use should be avoided within your components.  Components whose instances need to share data should consider using the `ThreadSafe` annotation (see below).

## Component Types

The first step in writing a custom component is to choose what type of component you need.  The component types are broken down by basic function.  Almost all components you write will be one of the first three (which are document transformers).  When creating a new component, choose the most specific type that meets your needs.

| Type | Description |
| --- | --- |
| `DocumentModifyingTransformer` | A document transformer that can do anything to the document passed to it.  It can delete, modify, and add fields to the document.  This transformer type also allows you to choose to drop the document. |
| `FieldValueCreatingTransformer` | A document transformer that creates new fields in the document based on existing fields. |
| `FieldValueModifyingTransformer` | A document transformer that modifies existing fields in the document.  This transformer type also allows you to choose to drop the document. |
| `MultiOutputDocumentTransformer` | An advanced document transformer that allows you to modify an existing "parent" document and to generate new "child" documents based on it.  The new documents will then flow through the system independent of the "parent" document. |
| `QueryTransformer` | A transformer that can modify queries before they are processed by the search engine. |
| `ResponseTransformer` | A transformer that can modify the resposnse to queries after they are processed by the search engine but before the response is returned to the user. |
| `BaseRoutingComponent` | An advanced component that can change the workflow that will be used for a system message. |
| `MessageHandlingWorkflowStage` | An advanced catch-all component that operates on raw system messages, doing whatever it likes to them. |


## The Mix-In Interfaces

Once you have chosen a component type, you can also add a number of mix-in interfaces to the component.  These allow you to indicate additional capabilities or requirements to the platform for your component.

### Lifecycle

| Name | Description |
| --- | --- |
| `Startable` | Provides a hook for the component to do initialization after its properties have been set before it does any processing. |
| `Stoppable` | Provides a hook for the component to clean up resources before system shutdown. |
| `AfterAllLocalInstancesStarted` | Provides a hook for the component to do initialization after all instances of this component have been started (`Startable.startComponent()` has been called). |
| `AfterLocalNodeStartup` | Provides a hook for the component to do initialization after all components in the system have been started. |

### Component Configuration

| Name | Description |
| --- | --- |
| `HasBackoffLocaleProperty` | |
| `HasCaseModeProperty` | |
| `HasDropDocumentOnExceptionProperty` | |
| `HasFieldMappingProperty` | |
| `HasFieldsProperty` | |
| `HasInputListProperty` | |
| `HasInputProperty` | |
| `HasOverwriteProperty` | |
| `HasQueryLanguageProperty` | |
| `HasSchemaNameProperty` | |
| `HasTokenizerProperty` | |

### Miscellaneous

| Name | Description |
| --- | --- |
| `AieLoggerAware` | No longer recommended.  Use [slf4j APIs](https://www.slf4j.org/api/org/slf4j/Logger.html) instead |
| `ComponentNameAware` | |
| `ProvidesProcessingFeedback` | |
| `QualifiedComponentNameAware` | |
| `SchemaUtilAware` | |
| `SystemEventPublisherAware` | |

### Annotations

| Name | Description |
| --- | --- |
| `MultiOutputDocumentTransformerMode` | |
| `SingleInstancePerCluster` | |
| `SingleInstancePerNamedComponent` | |
| `SingleInstancePerNode` | |
| `ThreadSafe` | |

## Testing your component

It is important to write focused and concise unit tests for your custom components.  Attivio provides a number of testing utilities and mock implementations to make writing good unit tests simple.  This archetype generation referenced by the [README](https://github.com/attivio/sdk/blob/5.2/README.md) page provides examples of the techniques described here.

##### Create the component

    MyComponent component = new MyComponent();

##### Configure your component

    // some example properties
    component.setRate(20.3);
    component.setLabel("label");

##### Optionally "start" your component

If your component uses any of the *lifecycle* or *miscellaneous* mix-ins, there is a test utility that will call them and set them up with appropriate mock implementations as needed:

    SdkTestUtils.startTransformer(component);

##### Create a sample document to use in your test

    IngestDocument doc = new IngestDocument("doc1");
    doc.setField("text", "some text");
    doc.setField("cost", 2800.23);

##### Process the document with your component

    SdkTestUtils.processDocument(doc, component);

##### Assert conditions on the document

    Assert.assertTrue(doc.containsField("newField"));

