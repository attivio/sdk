# Attivio 5.5 SDK

To get started using the SDK, use Maven (`mvn`) to generate a sample
client project or module.
Attivio modules allow custom code (most commonly ingestion or query transformers)
to be added to your Attivio projects.

An Attivio client project contains code that connects to an existing
Attivio system and ingests data, runs queries, or uses other public APIs.

[Public site for SDK javadoc](https://attivio.github.io/sdk-5.5-javadoc/index.html)

## Create a sample Attivio SDK project

### Version 5.5.0

```
mvn archetype:generate -DarchetypeGroupId=com.attivio.platform.archetypes -DarchetypeArtifactId=attivio-archetype-module -DarchetypeVersion=5.5.0.5
```

### Version 5.5.1

```
mvn archetype:generate -DarchetypeGroupId=com.attivio.platform.archetypes -DarchetypeArtifactId=attivio-archetype-module -DarchetypeVersion=5.5.1.2
```

[Attivio Module SDK](https://github.com/attivio/sdk/blob/5.5/attivio_module_sdk.md)

## Attivio Service Factory

- [Using the ServiceFactory](https://github.com/attivio/sdk/blob/5.5/service_factory.md)
- [Testing with the ServiceFactory](https://github.com/attivio/sdk/blob/5.5/testing_service_factory.md)
- [Creating a Custom Service](https://github.com/attivio/sdk/blob/5.5/creating_a_custom_service.md)

## Other guides

- [Writing and Testing Custom Components](https://github.com/attivio/sdk/blob/5.5/writing_and_testing_components.md)
- [Creating a Custom Executable](https://github.com/attivio/sdk/blob/5.5/creating_a_custom_executable.md)

***
[License Agreement](https://github.com/attivio/sdk/blob/5.5/license.md)
