[PlantUML](https://plantuml.com/) is a text embeddable UML diagramming tool that uses a simple markup language to generate UML diagrams that are then embedded into the markdown document.

![Markdown Monster PlantUML Support](https://github.com/RickStrahl/ImageDrop/blob/master/MarkdownMonster/PlantUML.gif?raw=true)

You can embed PlantUML blocks using* uing the following code block syntax used by many common Markdown platforms (including GitHub):

* Code block syntax: `` ```plantuml`` to delineate the PlantUML block

> PlantUML has to be enabled in the settings via the `Markdown.UsePlantUml` configuration switch in your settings. 

### Codeblock Syntax
Codeblock syntax uses the triple tick prefix You can use code block syntax if the editor misformatting becomes an issue.

![](/images/PlantUmlCodeBlockSyntax.png)

This syntax supports any of the flavors that are supported by the PlantUML server.

### Configuration Settings
In order to use PlantUML you have to enable it first via the `Markdown.UsePlantUml` setting, which can be set in the UI Settings or the JSON configuration file.

There are two settings available:

* **UsePlantUml**  
Determines whether PlantUML rendering is enabled or not.

* **PlantUmlLServerUrl**  
The server base URL that is used to render the diagram. This allows you a few options to specify a different server or for changing the output mechanism from the default `/svg/` to `/png/` for example. 

The default server url is:

```
http://www.PlantUML.com/PlantUml/png/
```

You can switch the `/png/` for other output formats such as `/svg/` to generate images or `/txt/` to generate ASCII art text.


### More about PlantUML Server

You can find out more about the PlantUML public server and how you can run your own local instance.

## Resources

* [PlantUML Site](https://PlantUML.com)
* [PlantUML Online Server and Playground](https://www.PlantUML.com/PlantUML/uml/SyfFKj2rKt3CoKnELR1Io4ZDoSa70000)
* [Plant UML Examples](https://real-world-PlantUML.com/)
* [Running a local copy of PlantUML](https://PlantUML.com/starting)