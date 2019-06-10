# Custom Executables

Custom executable functionality can be added to an Attivio project and/or install such that, by entering a command, a user can execute custom code as part of the attivio environment but in a separate process.

### Implementing `AttivioRunnable`

`AttivioRunnable` is an interface much like `java.lang.Runnable` in that it has an abstract run method. A class implementing `AttivioRunnable` and supplying a body for that run method can be run using the aie-exec executable in the `bin` directory of any Attivio installation. In order to take command line arguments to the executable, this class must have getters and setters for all fields to be obtained through the command line. The getters should be annotated with `@ConfigurationOption` so that they can be given certain properties as command line arguments such as description, whether or not they are required, and short option for specification. See a sample custom runnable below:

```java
@ConfigurationOption(description="This writes messages to the log file")
public class MyAttivioRunnable implements AttivioRunnable {
  private String message;

  public int run() throws AttivioException {
    Logger.getLogger(MyAttivioRunnable.class).info(message);
  }

  @ConfigurationOption(optionLevel=OptionLevel.Required, shortOpt="m", description="This message will be written to the log file")
  public String getMessage() {
    return message;
  }

  public void setMessage(String message) {
    this.message = message;
  }
}
```

### Registering the Custom Executable the Module

Any executable classes created in the manner above should be registered in the 'executables' field in the `attivio.module.json` file. The attivio module sdk documentation has more information on this

### Calling an `AttivioRunnable`

If everything is configured properly as described above, the custom executable should show up in the list of executables available from `aie-exec`:

```text
> ./aie_install/bin/aie-exec -h
...
Configured executables:
  myExecutable - This writes messages to the log file
    (com.myapp.MyAttivioRunnable)
...
> ./aie_install/bin/aie-exec myExecutable -h
...
Command Line Options:
 -m, --message <arg>    This message will be written to the log file
...
> ./aie_install/bin/aie-exec myExecutable -m "hello to the log file"
```

