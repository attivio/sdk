---
description: >-
  This is a glossary of the main interfaces and classes relevant to scanner
  implementation.
---

# Glossary

| Class/Interface | Description |
| :--- | :--- |
| `com.attivio.sdk.scanner.DataSourceScanner` | The interface every scanner must implement.  |
| `com.attivio.sdk.connector.DocumentPublisher` | The interface used by the scanner to create and delete documents and principals.   |
| `com.attivio.sdk.ingest.IngestDocument` | The document create by the scanner and fed through the `DocumentPublisher`.   |
| `com.attivio.sdk.schema.FieldNames` | The names of standard Attivo fields. These fields are already defined in the schema.   |
| `com.attivio.sdk.client.IngestionHistoryApi` | Service that allow the scanner to persist and retrieve the scanner state across runs.   |
| `com.attivio.sdk.scanner.IncrementalDataSourceScanner` | The scanner should implement this interface when incremental scan is required.  |
| `com.attivio.sdk.security.*` | Model classes to create principals and ACLs in order to control who is allowed to read Attivio documents.   |
| `com.attivio.sdk.server.annotation.*` | Use annotations define the administration UI for scanners and other Attivio components.   |



