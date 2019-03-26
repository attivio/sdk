# Attivio Module SDK

## Module generation

A new module can be generated using the maven archetype command.  Generated modules follow maven conventions for code and resource file locations.

```
mvn archetype:generate -DarchetypeGroupId=com.attivio.platform.archetypes -DarchetypeArtifactId=attivio-archetype-module -DarchetypeVersion=<archetype-version>
```

The value of `<archetype-version>` will depend on the version of Attivio SDK the new module will be built against.
See the [README](https://github.com/attivio/sdk/blob/5.5/README.md#create-a-sample-attivio-sdk-project) for details.

This interactive command asks for a few parameters to drive the creation of the module:

| Parameter | Description |
| --- | --- |
| groupId | The maven groupId for the new module.  For example `com.attivio.platform`. |
| artifactId | The maven artifactId for the new module.  This should be thought of as the module name.  The generated project will be in a directory with this name. |
| version | The version for the new module. It should follow the standard Maven versioning format. If no version is specified, the default of `0.1.0-SNAPSHOT` will be used.

## Building the module

The generated module can be built without any changes.  It includes working components and tests.  Enter the module directory and run `mvn`:

    mvn clean install

This will create a new jar in the target directory of your module.

## Using your new module

Modules can be added to your Attivio installation (in which case they _must_ be installed on every Attivio host) or added to projects which wish to use them.  To create a project with your new module without installing it, supply the jar to the createproject command as if it were a module name:

    createproject -n project-name -m module-dir/target/module-name-1.0-SNAPSHOT.jar

To add your module to your installation, the module zip or jar should be installed by running `aie-exec moduleManager`.  This program can list, install, and remove add-on modules.

## Module resources

```
src/main/resources $ tree
.
├── attivio.module.json
├── module-name
    ├── beans.xml
    ├── features.xml
    ├── module.xml
    └── module-name.properties
```

### The attivio.module.json file

The `attivio.module.json` file is located in a module's `src/main/resources` directory.  This file contains metadata about the module, including a description and declaration of the module's components, executables, and connectors.  Module metadata is also used during the module installation process to add and remove files to the Attivio installation.  The minimum metadata file is:

    {
      "name" : "module-name"
    }

Format:

| Field | Type | Description |
| --- | --- | --- |
| components | [String] | A list of component classes defined by the module. |
| connectors | {String,String} | A map of connector name to the java class which implements the connector. |
| dependencies | [String] | A list of modules upon which this module depends. Any module listed will be added to the project by the `createproject` tool automatically. |
| description | String | Description of the module |
| executables | {String,String} | A map of executable name to a java class extending `AttivioRunnable`.  The name will then be accessible when using `aie-exec`. |
| filesToDelete | [String] | A list of file names that will be removed from the installation.  File names are relative to the Attivio installation directory.  All 'removed' files are actually backed up to the module so that they may be restored if the module is removed. |
| licensed | boolean | Whether or not use of this module requires an additional license. |
| minimumPatchLevel | int | A number indicating the minimum patch that must be installed in order to install the module. |
| moduleVersion | String | Version string for the module, using the Semantic Versioning [specification](http://semver.org/).  Module versions are independent of the Attivio platform version.  In particular, modules with a major version of 0 (e.g., 0.1.3) are experimental and unstable with respect to API.  Support of such modules is not part of Attivio standard support and requires a specific addendum or SOW. |
| name | String | Name of the module |
| newFiles | {String,String} | A map of new files to be installed.  The key specifies a Attivio installation relative path to be linked to a module relative path that is supplied by the module.  If the key path exists it will be backed up in the module for later restoration if the module is removed. |
| requiredPlatformVersion | String | A version requirement specification String.  The platform version must match in order to install the module.  A plain version number (e.g. `5.2.6`) requires an exact match.  `>`, `<`, `>=`, and `<=` may be used for specifying ranges.  For example `>=5.2` will match any version >= to `5.2`, including `5.2.6`, `5.5`, and `6.0`.  A range may be specified by including a second condition.  For example `>=5.2.6 <6` will allow any 5 release after 5.2.6 and before 6.0.  Full details available [here](https://github.com/zafarkhaja/jsemver#semver-expressions-api-ranges) |

Example:

    {
      "name":"cloudera-5.10.1",
      "moduleVersion":"0.1.0",
      "requiredPlatformVersion":">=5.2.6",
      "minimumPatchLevel":0,
      "description":"Replaces default Hadoop libraries with Cloudera 5.10.1 version",
      "filesToDelete":[
        "lib/hadoop-annotations-2.7.2.jar",
        "lib/hadoop-annotations-2.7.3.jar"
      ],
      "newFiles":{
        "lib/hadoop-annotations.jar":"lib/hadoop-annotations-2.6.0-cdh5.10.1.jar"
      }
      "components":[
        "com.attivio.Component1",
        "com.attivio.Component2"
      ]
    }

This module will supply a new version of the hadoop-annotation jar, by creating a softlink from `ATTIVIO_HOME/lib/hadoop-annotations.jar` to `ATTIVIO_HOME/modules/cloudera-5.10.1/lib/hadoop-annotations-2.6.0-cdh5.10.1.jar`.  Files `ATTIVIO_HOME/lib/hadoop-annotations-2.7.2.jar` and `ATTIVIO_HOME/lib/hadoop-annotations-2.7.3.jar` will be moved to a backup directory for later restoration if they exist.  This module does not care about patch level, but does require that the Attivio version is 5.2.6 or later.

## Adding your module to source control

Any module worth writing should be added to source control!  Use github's [excellent documentation](https://help.github.com/articles/adding-an-existing-project-to-github-using-the-command-line/) to add your module to a github repository.
1.
