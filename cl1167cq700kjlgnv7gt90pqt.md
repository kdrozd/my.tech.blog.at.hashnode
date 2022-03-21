## Do I need DSL

I need to sparkle some metadata on my classes. There are some ways in Java to do it. 

I plan to have something close to 500k classes. That's a lot. They will provide some specific functionalities. On top of functional code, I need to add some metadata to each of them to provide "managed functionalities". 

## Keep metadata close to code

There are a few ways to do it, keeping metadata close to the main code. This gives a lot of convenience as code and data can be kept in the same editor and edited at the same time. To be honest, I like this approach.

### Interfaces and abstract classes

The first thing that can be done is to create an interface or abstract class and implement abstract/interface methods for each class.

```
// File EntityDocumentation.java
public interface EntityDocumentation {
    public String description();
    public String system();
    public Flags flags();
}

// File EntityClass.java
public class EntityClass implements EntityDocumentation {
   // Some logic and code
   
   public String description(){
     return "Super class";
   }
   public String system(){
     return "online";
   }
    public Flags[] flags(){
      return new Flags[]{Flag.A, Flag.B};
   }

}
```

Similar code can be implemented using abstract classes, but interfaces are probably a better choice. 

Such code can be processed later using reflection to get metadata and do something with them. 



Examples:
- https://www.burningwave.org/how-to-find-all-classes-that-implement-one-or-more-interfaces/
- https://www.burningwave.org/finding-all-classes-that-extend-a-base-class/

### Annotations

This is the way. Probably the most popular approach in the Java world, Swagger/OpenAPI are great examples, and they are very close to what I'm trying to do.

```
@OpenAPIDefinition(
    tags = {
            @Tag(name="widget", description="Widget operations."),
            @Tag(name="gasket", description="Operations related to gaskets")
    },
    info = @Info(
        title="Example API",
        version = "1.0.1",
        contact = @Contact(
            name = "Example API Support",
            url = "http://exampleurl.com/contact",
            email = "techsupport@example.com"),
        license = @License(
            name = "Apache 2.0",
            url = "https://www.apache.org/licenses/LICENSE-2.0.html"))
)
public class ExampleApiApplication extends Application {
}
```
This will generate json or yaml file with OpenAPI description. 

This is more natural but require some work upfront as all these annotations have to be created. Then some logic to process them in form of runtime processing or annotation processors.


## Externalize metadata

Sometimes it's not possible to implement an interface or add annotations to a class, especially when it's an external dependency. In this case, I would use some external files to provide metadata and use to bind them to the main code. 

### The easy way

Nothing fancy. Use TOML, YAML, JSON or just properties files to add anything you need in some well-defined way. Throw some of your favourite deserialization library, and you are done. If you put structure to any text format, and you are getting DSL (dam silly language)© After deserialization such data can be processed as usual. In JSON they can be stored in many databases.

## Textual DSL - Domain Specific Language

![Xtext - grammar definition (part of it)](https://cdn.hashnode.com/res/hashnode/image/upload/v1647893334080/s7p_1UpLl.png)

Now we are speaking with big bois, I played with [Xtext](https://www.eclipse.org/Xtext/documentation/102_domainmodelwalkthrough.html) and I like it very much. Languages can do anything from code generation to building simple general-purpose languages. Tooling support is legendary but can be minus if you don't like Eclipse (I do), but native support for LSP can make it work with many editors. 

Still, the design and implementation of non-trivial language take "few days". 

Xtext is not the only one, but more practical (in development) is my go-to choice. https://langium.org/ may be another one soon.

## Projectional DSL


![language-support.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1647894381779/Rw4WCR1B-.png)
Usually, if you have a problem and try to solve it with Java you have 


![Zrzut ekranu z 2022-03-21 21-18-45.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1647893947654/M_4zMLcRL.png)

Don't get me wrong, [Meta Programming System](https://www.jetbrains.com/mps/) is great, and I've to mention it on this list. But that's huge overkill for my problem and most of yours.

It helps to build languages where there are no limits, look what they did to `C`: http://mbeddr.com/.

## What to use.

All contestants have good and bad points. But as I would love to have nice DSL to support my project, I can't afford it. For now, I'll be the one that will have to build it and put the data. Code and metadata will have to be together as there is no practical benefit of DSL and tool support that annotations in Java will not give me, additional reassurance comes out of counting how many projects uses DSL vs annotations and are targeted to technical people/developers.


ps.

I'm looking forward to Xtext/MSP projects, so stay tuned. 














 

