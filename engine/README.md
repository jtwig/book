# Jtwig Core

<p style="text-align: justify;">
Within this section one will detail how to work with Jtwig at it's core API. As a template engine, Jtwig has three main concepts, they are <b>Environment</b>, <b>Resource</b> and <b>Model</b>.
</p>

```
Output = (Environment, Resource, Model)
```

<p style="text-align: justify;">
The <b>Environment</b> contains all Jtwig configurations and predefined behaviour, this includes possible extensions that might be added. The <b>Resource</b> contains the intermediate Jtwig representation, also known as Template and the <b>Model</b> is the container of key and value pairs which combined with the Template generates the output. We can break it down in the following way.
</p>

```
Template = (Environment, Resource)
```

<p style="text-align: justify;">
Where, basically, the <code>Template</code> is the combination of the <b>Environment</b> with the <b>Resource</b>. This has special meaning when extensions are added and means some intermediate representations don't mean anything without the proper extension added to the <b>Environment</b>. Note that, one will detail about Extensions later on.
</p>

```
Output = (Template, Model)
```

### Hello World Example

<p style="text-align: justify;">
Let's now have a look at the famous Hello World program in Jtwig using the core API.
</p>


```java
// Environment
EnvironmentConfiguration configuration = new DefaultEnvironmentConfiguration();
EnvironmentFactory environmentFactory = new EnvironmentFactory();
Environment environment = environmentFactory.create(configuration);

// Resource
Resource resource = new StringResource("Hello {{ token }}!");

// Template
JtwigTemplate jtwigTemplate = new JtwigTemplate(environment, resource);

// Model
JtwigModel model = JtwigModel.newModel().with("token", "World");

// Output
String output = jtwigTemplate.render(model);
```

<p style="text-align: justify;">
As one can see, the way Jtwig core API is built follows the same concepts mentioned before, where the <b>Enviornment</b> and <b>Resource</b> are first instantiated in order to create the <code>JtwigTemplate</code>, which when combined with the <code>JtwigModel</code> generates the output.
</p>

**Jtwig Model**

<p style="text-align: justify;">
Jtwig Model can be seen as a map of properties, which will then be used to render the template. The keys can only be valid Java identifiers as mentioned before.
</p>

```java
JtwigModel model = JtwigModel.newModel()
     .with("variable", "Jtwig")
     .with("secondVariable", 1);
```

### Processing Pipeline

**Parsing Stage**

<p style="text-align: justify;">
The way Jtwig produces the final result is through a well defined processing pipeline. At start of this whole processing is the parsing stage. The parsing stage is where Jtwig parses a file producing a tree of nodes based of the Jtwig Abstract Syntax Tree. This tree is composed of content nodes and expressions. As mentioned before expressions are evaluated to values, and where content nodes are evaluated to streamable content. By content nodes we mean all the Jtwig tags and raw text defined in the template.
</p>

**Lazy loading nested resources**

<p style="text-align: justify;">
In Jtwig nested resources, which can be referred using <code>include</code>, <code>extends</code>, <code>embed</code> and <code>import</code> constructs, are loaded in rendering time (lazy loaded) as the path expression needs to be evaluated first.
</p>

**Caching resources**

<p style="text-align: justify;">
Another concept included in the parsing stage is the resource caching mechanism. By default Jtwig will cache the parsed resources in memory in a persistent fashion, that means, for the lifetime of the JVM, resources are only parsed once. 
</p>

**Rendering Stage**

<p style="text-align: justify;">
The next stage is the rendering stage. Each content node in the parsed tree is processed into streamable content. Before each content node being rendered the associated escape mode is initialised. This will then be used to serialize the output. The Jtwig serializer is capable of escaping content based on a specified strategy. Supported escape modes were already specified in the <code>autoescape</code> tag definition.
</p>

**Expression Evaluation**

<p style="text-align: justify;">
During the rendering stage, expressions are evaluated, for example, to perform the Jtwig control flow. An important aspect of this evaluation mechanism is a special type introduced by Jtwig, that is, the <code>Undefined</code> value. It's a singleton used to specify when the result of evaluating an expression is undefined. For example, accessing an undefined array index or evaluating an undefined variable.
</p>
