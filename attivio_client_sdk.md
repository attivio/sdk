## Client generation

A new client project can be generated using the maven archetype command.  Generated modules follow maven conventions for code and resource file locations.

    mvn archetype:generate -DarchetypeGroupId=com.attivio.platform.archetypes -DarchetypeArtifactId=attivio-archetype-client -DarchetypeVersion=5.2.6.1

This interactive command asks for a few parameters to drive the creation of the module:

| Parameter | Description |
| --- | --- |
| groupId | The maven groupId for the client project.  For example, `com.attivio.platform`. |
| artifactId | The maven artifactId for the client project.  The generated project will be in a directory with this name. |
| hadoop | Whether or not to include dependencies and samples for running against Attivio running on a Hadoop cluster. |
