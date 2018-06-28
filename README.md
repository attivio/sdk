# Attivio SDK
To get started using the SDK, use Maven (`mvn`) to generate a sample client project or module.  Attivio modules allow custom
code (most commonly ingestion or query transformers) to be added to your Attivio projects.  An Attivio client project contains
code that connects to an existing Attivio system and ingests data, runs queries, or uses other public APIs.

[Public site for SDK javadoc](https://attivio.github.io/unpublished/index.html)

## Create a sample Attivio SDK project

    mvn archetype:generate -DarchetypeGroupId=com.attivio.platform.archetypes -DarchetypeArtifactId=attivio-archetype-module -DarchetypeVersion=5.6.0.0

[Attivio Module SDK](attivio_module_sdk.md)

## Attivio Service Factory

[Using the ServiceFactory](service_factory.md)  
[Testing with the ServiceFactory](testing_service_factory.md)  
[Creating a Custom Service](creating_a_custom_service.md)  

## Other guides

[Writing and Testing Custom Components](writing_and_testing_components.md)  
[Creating a Custom Executable](creating_a_custom_executable.md)  
[Writing and Testing Data Source Scanners](writing_and_testing_scanners.md)  



***
[License Agreement](license.md)
