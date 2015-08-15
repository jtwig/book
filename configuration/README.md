# Configurations

<p style="text-align: justify;">
Jtwig is highly configurable, it allows one to setup the very basis of the language, at it's syntax level, to plugin new functionalities using extensions. In this section we will specify all properties and it's possibilities about Jtwig configuration.
</p>

**How to customize**



### Parser Configuration

<p style="text-align: justify;">
Starting with the very basic Parser configuration. Listed below is the list of properties one can provide.
</p>

**Input Charset** 

<p style="text-align: justify;">
Defines the input charset to use when reading input binary streams as text. By default is set to the Java default charset <code>Charset.defaultCharset()</code>, check Java documentation for details.
</p>

```java
EnvironmentConfigurationBuilder.configuration()
    .parser()
        .withInputCharset(Charset.forName("UTF-8"))
    .and().build();
```

**Syntax Configuration** 

<p style="text-align: justify;">
This property allows one to define the syntactic symbols, they are:
</p>

- Start Comment, by default `{#`
- End Comment, by default `#}`
- Start Output, by default `{{ '{{' }}`
- End Output, by default `{{ '}}' }}`
- Start Code, by default `{{ '{%' }}`
- End Code, by default `%}`

**Unary Operators** 

<p style="text-align: justify;">
Unary operators to use in Jtwig, this is a way to plug in extra unary operators, the default unary operators were already specified before.
</p>

**Binary Operators** in a similar way as Unary Operators, one can extend Jtwig by providing extra binary operators through configuration.
**Template Cache Provider** one can define a cache provider which will cache parsed templates as a way to increase the overall speed of rendering a Jtwig template.
**Addon Parsers** is a way to plug in extra Jtwig constructs.