# Render Extension

<p style="text-align: justify;">
The render extension, only available for web apps, enables users to embed the result of rendering a given path. It can be seen as another way to include other resources available throught HTTP GET endpoints. This extension exposes a new tag <code>render</code>.
</p>

**``render`` tag**

<p style="text-align: justify;">
The render tag is expecting a path to an internal resource and, optionally, a map of parameters. It will then create a new <code>HttpServletRequest</code> with the parameters provided in memory and ask the <code>RequestDispatcher</code> to include the resource with the given path.
</p>

```twig
{% render '/hello' with {name: 'Jtwig'} %}
```

<p style="text-align: justify;">
The example above will make a call to render the servlet listening on the path <code>/hello</code> with the GET parameters <code>name=Jtwig</code>.
</p>

### Configuration

<p style="text-align: justify;">
As shown below, the configuration of this extension is none. One just need to pass it on to the Environment configuration so it will be used.
</p>

```java
EnvironmentConfigurationBuilder.configuration()
                .extensions().add(new RenderExtension()).and()
                .build()
```



### Integration

<p style="text-align: justify;">
Integrating Jtwig Render Extension on your project is quite simple with the help of dependency managers. To check the most recent version, go to <a target="_blank" href="https://bintray.com/jtwig/maven/jtwig-render-extension/view">bintray</a>.
</p>

**Gradle**


```gradle
repositories {
    jcenter()
}
dependencies {
    compile 'org.jtwig:jtwig-render-extension:1.X'
}
```


**Maven**

```xml
<repositories>
    <repository>
        <id>bintray</id>
        <url>https://jcenter.bintray.com/</url>
    </repository>
</repositories>

<dependencies>
    <dependency>
        <groupId>org.jtwig</groupId>
        <artifactId>jtwig-render-extension</artifactId>
        <version>1.X</version>
    </dependency>
</dependencies>
```

**Examples**

<p style="text-align: justify;">
Check the <a href="https://github.com/jtwig/jtwig-examples">jtwig-examples</a> project on github for examples using this render engine.
</p>