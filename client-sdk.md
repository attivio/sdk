# Client SDK

A new client project can be generated using the maven archetype command. Generated projects follow maven conventions for code and resource file locations.

```text
mvn archetype:generate \
  -DarchetypeGroupId=com.attivio.platform.archetypes \
  -DarchetypeArtifactId=attivio-archetype-client \
  -DarchetypeVersion=4.4.2.0
```

This interactive command asks for a few parameters to drive the creation of the module:

| Parameter | Description |
| :--- | :--- |
| `groupId` | The maven groupId for the new module.  For example `com.attivio.platform`. |
| `artifactId` | The maven artifactId for the new module.  This should be thought of as the module name.  The generated project will be in a directory with this name. |
| `version` | The version for the new module. It should follow the standard Maven versioning format. If no version is specified, the default of `1.0.0-SNAPSHOT` will be used. |

