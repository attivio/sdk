# Testing Components

It is important to write focused and concise unit tests for your custom components. Attivio provides a number of testing utilities and mock implementations to make writing good unit tests simple. This archetype generation referenced by the README page provides examples of the techniques described here.

## Create the component

```java
MyComponent component = new MyComponent();
```

## Configure your component

```java
// some example properties
component.setRate(20.3);
component.setLabel("label");
```

## Optionally "start" your component

If your component uses any of the _lifecycle_ or _miscellaneous_ mix-ins, there is a test utility that will call them and set them up with appropriate mock implementations as needed:

```java
SdkTestUtils.startTransformer(component);
```

## Create a sample document to use in your test

```java
AttivioDocument doc = new AttivioDocument("doc1");
doc.setField("text", "some text");
doc.setField("cost", 2800.23);
```

## Process the document with your component

```java
SdkTestUtils.processDocument(doc, component);
```

## Assert conditions on the document

```java
Assert.assertTrue(doc.containsField("newField"));
```

