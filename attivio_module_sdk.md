# Attivio Module SDK

## Module generation

A new module can be generated using the maven archetype command.  Generated modules follow maven conventions for code and resource file locations.

    mvn archetype:generate -DarchetypeGroupId=com.attivio.platform.archetypes -DarchetypeArtifactId=attivio-archetype-module -DarchetypeVersion=0.1.0

This interactive command asks for a few parameters to drive the creation of the module:

| Parameter | Description |
| --- | --- |
| groupId | The maven groupId for the new module.  For example `com.attivio.platform` |
| artifactId | The maven artifactId for the new module.  This should be thought of as the module name.  The generated project will be in a directory with this name |
| includeWeb | Whether or not include examples that include a Attivio Admin UI insert.  These examples use unsupported API and require Attivio to be installed. |

## Building the module

The generated module can be built without any changes.  It includes working components and tests.  Enter the module directory and run `mvn`:

    mvn clean install

This will create a new jar in the target directory of your module.

## Using your new module

Modules can be added to your Attivio installation (in which case the _must_ be installed on every Attivio host) or added to projects which wish to use them.  To create a project with your new module without installing it, supply the jar to the createproject command as if it were a module name:

    createproject -n project-name -m module-dir/target/module-name-1.0-SNAPSHOT.jar

## Module resources

```
src/main/resources $ tree
.
├── attivio.module.xml
├── module-name
│   ├── beans.xml
│   ├── features.xml
│   ├── module.xml
│   └── module-name.properties
└── webapps
    └── module-name
        └── WEB-INF
            ├── classes
            │   └── templates
            │       └── module-name.vm
            └── web.xml
```

### The attivio.module.xml file

The `attivio.module.xml` file is located in a module's `src/main/resources` directory.  This file contains metadata about the module, including a description and declaration of the module's components, executables, and connectors.

