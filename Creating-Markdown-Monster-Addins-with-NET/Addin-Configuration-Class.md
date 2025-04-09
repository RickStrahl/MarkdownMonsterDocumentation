Configuration is a key component to most applications and a Markdown Monster addin is not exception. Markdown Monster provides an easy way to create a custom configuration for your Addin.

The Markdown Monster Visual Studio Project Template automatically creates a configuration class for you. You can add properties to this class that act as configuration values that can be easily persisted and restored in a JSON configuration file.


### The Configuration Class
This class can contain any properties including nested objects for complex configuration setups. Each of the properties - including nested ones - are persisted and read from the backing JSON file.

A Configuration class looks something like this:

```cs
public class KavaDocsConfiguration : 
             BaseAddinConfiguration<KavaDocsConfiguration>
{
    public KavaDocsConfiguration()
    {
        // specify the name of the file
        // created in the MM common settings folder
        ConfigurationFilename = "KavaDocsAddin.json";
    }
    
    public string LastProjectFile { get; set; }
    public bool OpenLastProject { get; set; }
    public string LastImageFolder { get; set; }
    public int StatusMessageTimeout { get; set; } = 6000;
}
```

You can use this class to add properties that can be persisted easily into a JSON configuration file.

### Accessing the Configuration Setting via Singleton
By default this configuration class will be in `<addinName>Configuration.cs`. To access this class simply use:

```cs
// Automatically initialized and reads values on first access
var config = SampleAddinConfigration.Current;

SampleAddinConfigration.Current.MySetting = MySetting
...
var setting = SampleAddinConfigration.Current.MySetting;
```

Accessing the configuration object automatically loads any stored property settings from the configuration file. 

### Persist Configuration Settings to File
You can also save settings back to the configuration file:

```cs
SampleAddinConfigration.Current.Write()
```

Persisted values are automatically read the next time the configuration class is initialized.

You can also explicitly re-read values with:

```cs
SampleAddinConfigration.Current.Read()
``