# Attivio SDK
To get started using the SDK, use Maven (`mvn`) to generate a sample client project or module.  Attivio modules allow custom
code (most commonly ingestion or query transformers) to be added to your Attivio projects.  An Attivio client project contains
code that connects to an existing Attivio system and ingests data, runs queries, or uses other public APIs.

## Create a sample Attivio module 

    mvn archetype:generate -DarchetypeGroupId=com.attivio.platform.archetypes -DarchetypeArtifactId=attivio-archetype-module -DarchetypeVersion=4.4.0.0

[Attivio Module SDK](attivio_module_sdk.md)

## Create a sample Attivio client project

    mvn archetype:generate -DarchetypeGroupId=com.attivio.platform.archetypes -DarchetypeArtifactId=attivio-archetype-client -DarchetypeVersion=4.4.0.0

[Attivio Client SDK](attivio_client_sdk.md)

## Other guides

[Writing and Testing Custom Components](writing_and_testing_components.md)
    