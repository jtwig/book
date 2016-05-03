# Json Extension

<p style="text-align: justify;">
The JSON extension adds Jtwig the capability of converting Java objects to a String JSON representation. It includes a function <code>json_encode</code> to perform such operation.
</p>

```twig
{{ json_encode(object) }}
```

<p style="text-align: justify;">
Under the wood, jtwig json extension will, using the configured mapper, convert the given object into a string.
</p>

### Configuration

```java
EnvironmentConfigurationBuilder
    .configuration()
        .extensions()
            .add(new JsonExtension(JsonMapperProviderConfigurationBuilder
                .jsonConfiguration()
                .build())
            )
        .and()
    .build()
```

<p style="text-align: justify;">
The configuration allows one to define multiple <code>JsonMapperProvider</code>, which supplies an instance of a mapper. The first use of the function <code>json_encode</code> will cause the mapper to be resolved and stored as singleton. Jtwig iterates over the list of <code>JsonMapperProvider</code> where the first one resolving will be used. By default, Jtwig defines two <code>JsonMapperProvider</code>, the <code>Jackson2JsonMapperProvider</code> and <code>JacksonJsonMapperProvider</code> which use, respectively, Jackson version 2 and 1.
</p>



### Integration

<p style="text-align: justify;">
Integrating Jtwig JSON Extension on your project is quite simple with the help of dependency managers. To check the most recent version, go to <a target="_blank" href="https://bintray.com/jtwig/maven/jtwig-json-extension/view">bintray</a>.
</p>

**Gradle**


```gradle
repositories {
    jcenter()
}
dependencies {
    compile 'org.jtwig:jtwig-json-extension:1.X'
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
        <artifactId>jtwig-json-extension</artifactId>
        <version>1.X</version>
    </dependency>
</dependencies>
```

**Examples**

<p style="text-align: justify;">
Check the <a href="https://github.com/jtwig/jtwig-examples">jtwig-examples</a> project on github for examples using this render engine.
</p>