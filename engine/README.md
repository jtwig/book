# Jtwig Core

<p style="text-align: justify;">
Within this section one will detail how to work with Jtwig at it's core. First, let's start defining a Jtwig Template.
</p>

>  A **Jtwig Template** is a pair containing a **resource** and an **environment**. Where the resource represents the intermediate Jtwig representation (the template itself) and the environment configured behaviour and properties used to render the template.

```java
// Jtwig Template Dependencies
Resource resource = new ...;
Environment environment = new ...;
// Jtwig Template Creation
JtwigTemplate jtwigTemplate = new JtwigTemplate(resource, environment);
```

## Resources

<p style="text-align: justify;">
Resources in Jtwig can be one of the following types:
</p>

- **`StreamResource`**, it's the most basic resource, it basically exposes a given stream as a Jtwig resource. Use this specific implementation with caution, be aware of `InputStream` statefull properties. Also this implementation has serious limitations when it comes to cache parsed Jtwig templates. Example:

```java
InputStream inputStream = new ...;
Resource resource = new StreamResource(inputStream);
```

- **`StringResource`**, a resource supporting Jtwig Template specifications using a Java String. This type of resource is useful to specify templates inlined with the code.

```java
Resource resource = new StringResource("Hello {{ variable }}!");
```

- **`FileResource`**, as the name can tell, uses a file as the reference to retrieve a Jtwig template.

```java
Resource resource = new FileResource(new File("<path to file>"));
```

- **`ClasspathResource`**, similar to a `FileResource` but useful when one want to render a template located in the application classpath. The classpath resource relies on the implementation of a `ClasspathResourceLoader`, which provides an interface for loading classpath resources and has a default implementation (`DefaultClasspathResourceLoader`).

```java
ClasspathResourceLoader classpathResourceLoader = new ...;
Resource resource = new ClasspathResource("<path>", classpathResourceLoader);
```

## Environment


<p style="text-align: justify;">
Environment contains all the configured behaviour while rendering Jtwig Templates. One will describe all possibilities of configuring Jtwig Environment in the Configurations section in the next charpters.
</p>

```java
EnvironmentConfiguration configuration = EnvironmentConfigurationBuilder
                .configuration()
                .build();
EnvironmentFactory environmentFactory = new EnvironmentFactory();
Environment environment = environmentFactory.create(configuration);
```

<p style="text-align: justify;">
One can see above how to create a an instance of environment using default configuration. It requires the <code>EnvironmentFactory</code> which then is given a <code>configuration</code>.
</p>

## Rendering

<p style="text-align: justify;">
In order to render a Jtwig Template, once an instance of it exists, one have two possibilities, either rendering it into a <code>String</code>, or to an <code>OutputStream</code>, both require a model to be given.
</p>

```java
JtwigTemplate jtwigTemplate = ...;
JtwigModel model = ...;
String result = jtwigTemplate.render(model);
```

<p style="text-align: justify;">
Note that, depending on the resource, the Jtwig Template, might be statefull therefore could not be used multiple times, for example, <code>StreamResource</code> is statefull, however, <code>StringResource</code>, <code>FileResource</code> and <code>ClasspathResource</code> are stateless.
</p>


```java
JtwigTemplate jtwigTemplate = ...;
JtwigModel model = ...;
OutputStream outputStream = ...;
jtwigTemplate.render(model, outputStream);
```

## Jtwig Model

<p style="text-align: justify;">
Jtwig Model can be seen as a map of properties, which will then be used to render the template.
</p>

```java
JtwigModel model = new JtwigModel()
     .with("variable", "Jtwig")
     .with("secondVariable", 1);
```

