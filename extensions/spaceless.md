# Spaceless Extension


<p style="text-align: justify;">
The spaceless extension is a tiny extension which add the <code>spaceless</code> tag construct to Jtwig. It works with HTML by default, allowing one to remove unnecessary whitespaces.
</p>

```twig
{% spaceless %}
<div>
    <label>Example</label>
</div>
{% endspaceless %}
```


<p style="text-align: justify;">
The previous example will produce <code>&lt;div&gt;&lt;label&gt;Example&lt;/label&gt;</div></code>
</p>

### Configuration

```java
EnvironmentConfigurationBuilder.configuration()
    .extensions()
        .add(SpacelessExtension.defaultSpacelessExtension())
    .and()
.build()
```

<p style="text-align: justify;">
The previous example will plugin the Spaceless extension with the default configuration. The only parameter to be configured is an instance of <code>SpaceRemover</code> which is used to remove the whitespaces from the content. By default this extension is configured to use the <code>HtmlSpaceRemover</code > implementation.
</p>


### Integration

<p style="text-align: justify;">
Integrating Jtwig Spaceless Extension on your project is quite simple with the help of dependency managers. To check the most recent version, go to <a target="_blank" href="https://bintray.com/jtwig/maven/jtwig-spaceless-extension/view">bintray</a>.
</p>

**Gradle**


```gradle
repositories {
    jcenter()
}
dependencies {
    compile 'org.jtwig:jtwig-spaceless-extension:1.X'
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
        <artifactId>jtwig-spaceless-extension</artifactId>
        <version>1.X</version>
    </dependency>
</dependencies>
```

**Examples**

<p style="text-align: justify;">
Check the <a href="https://github.com/jtwig/jtwig-examples">jtwig-examples</a> project on github for examples using this spaceless engine.
</p>