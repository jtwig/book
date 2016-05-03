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