
# Environment


<p style="text-align: justify;">
As mentioned before, the Environment contains all the configured properties and behaviour while rendering Jtwig Templates, it might include extensions as well. The simpliest way to instantiate an <code>Environment</code> object is with the following code.
</p>

```java
EnvironmentConfiguration configuration = new DefaultEnvironmentConfiguration();
EnvironmentFactory environmentFactory = new EnvironmentFactory();
Environment environment = environmentFactory.create(configuration);
```

<p style="text-align: justify;">
In order to create an <code>Environment</code> instance one need an <code>EnvironmentConfiguration</code> to be provided to the <code>EnvironmentFactory</code>.
</p>

## ``EnvironmentConfigurationBuilder`` API

<p style="text-align: justify;">
However, as shown in the previous example, the <code>DefaultEnvironmentConfiguration</code> creates an immutable <code>EnvironmentConfiguration</code> instance. To overcome that limitation and customize Jtwig configuration the <code>EnvironmentConfigurationBuilder</code> API was created. It comes with a set of methods to specify all possible Jtwig behaviour.
</p>

### Extending the default configuration

<p style="text-align: justify;">
An useful constructor of this builder is the prototype constructor which allows one to initialize the builder given an instance of an EnvironmentConfiguration. Specially useful when extending the default configuration (the most common scenario), instead of creating an entire new one.
</p>

```java
new EnvironmentConfigurationBuilder(new DefaultEnvironmentConfiguration())
                .build()
```

<p style="text-align: justify;">
The example above will create an instance of EnvironmentConfiguration copying all the definitions from the default configuration. One can then use the builder to modify the default configuration. Another way to achieve the same is by using the static method ``EnvironmentConfigurationBuilder::configuration``, which makes the previous code snippet equivalent to the following one.
</p>

```java
EnvironmentConfigurationBuilder.configuration().build()
```

### ``parser()``

<p style="text-align: justify;">
The <code>parser()</code> method returns an instance of <code>AndJtwigParserConfigurationBuilder</code>, such class was built for the purpose of configuring the Jtwig parser. Let's see an example of it.
</p>

```java
new EnvironmentConfigurationBuilder().parser()
                .syntax()
                    .withStartCode("{ %").withEndCode("%}")
                    .withStartOutput("{{").withEndOutput("}}")
                    .withStartComment("{#").withEndComment("#}")
                .and()
                .withAddonParserProvider(customAddonParser())
                .withBinaryOperator(customBinaryOperator())
                .withUnaryOperator(customUnaryOperator())
                .withCacheProvider(new NoTemplateCacheProvider())
                .and()
                .build();
```

<p style="text-align: justify;">
With this one can specify:
</p>

* ``StartCode``, ``EndCode``, ``StartOutput``, ``EndOutput``, ``StartComment`` and ``EndComment`` allows one customize the sintactic sumbols used by Jtwig code islands.
* ``AddonParserProvider``, ``BinaryOperator`` and ``UnaryOperator`` is the way to enhance the parser with extra addons, this will be detailed further on. All the mentioned methods are used to build lists of objects which means one can specify as many as we want.
* ``CacheProvider`` setting gives the user the possibility of configuring a cache system for compiled Jtwig templates speeding up the rendering. Such cache uses a **Resource** as key and provides the Jtwig compiled templates as value. By caching it, operations like reading files and flatening the template structure can get a significant performance boost. Jtwig core comes with three implementations:
    
1. ``NoTemplateCacheProvider`` where no cache is provided, this is the default behaviour.
2. ``PersistentTemplateCacheProvider`` provides a persistent cache mechanism, it's very execution time performant, however not memory efficient.
3. ``LimitedTemplateCacheProvider`` provides a simple [guava](https://github.com/google/guava/wiki/CachesExplained) cache implementation with the specified size.

### ``functions()``

<p style="text-align: justify;">
The <code>functions()</code> method returns an instance of <code>AndFunctionResolverConfigurationBuilder</code>, such class was built for the purpose of configuring the Jtwig function repository, this allows to inject function implementations into the environment.
</p>

```java
new EnvironmentConfigurationBuilder().functions()
                .withFunction(customFunction())
                .and()
                .build();
```

### ``resources()``

<p style="text-align: justify;">
The <code>resources()</code> method returns an instance of <code>AndResourceResolverConfigurationBuilder</code> used to build the resource resolver.
</p>

```java
new EnvironmentConfigurationBuilder().resources()
                .withFunction(customFunction())
                .and()
                .build();
```

<p style="text-align: justify;">
It's possible to specify multiple resources resolvers. Resource resolvers are detailed further on.
</p>

### ``render()``

<p style="text-align: justify;">
The <code>render()</code> method returns an instance of <code>AndRenderConfigurationBuilder</code> which provides a set of useful builder methods to configure the rendering, let's check the following example.
</p>

```java
new EnvironmentConfigurationBuilder()
                .render()
                    .withStrictMode(strictMode)
                    .withInitialEscapeMode(initialEscapeMode)
                    .withOutputCharset(outputCharset)
                .and().build();
```

<p style="text-align: justify;">
Here you can find the following properties:
</p>

* ``StrictMode`` sets the way to resolve variables in Jtwig, if strict mode is active, undefined variables will throw an exception when evaluated. However, if strict mode is disabled, it will be evaluated to ``Undefined.UNDEFINED``. Strict mode is disabled by default.
* ``InitialEscapeMode`` as the name says sets the initial escape mode, which by default is set to ``NONE``, which means, strings wont be escaped when rendering the template. Escape modes were already mentioned before (Tags > Commands).
* ``OutputChatset`` defines the default output charset for Jtwig.

### ``propertyResolver()``

<p style="text-align: justify;">
This method allows one to setup multiple property resolvers. It returns an instance of <code>AndPropertyResolverConfigurationBuilder</code>.
</p>

```java
new EnvironmentConfigurationBuilder()
                .propertyResolver()
                    .withPropertyResolver(propertyResolver)
                .and().build();
```

### ``listEnumeration()``

<p style="text-align: justify;">
The <code>listEnumeration()</code> method returns an instance of <code>AndEnumerationListStrategyConfigurationBuilder</code> allowing to configure the list enumeration stretagies. This strategies are used when resolving lists by comprehension in Jtwig. By default, and as mentioned before, Jtwig comes with four different strategies:
</p>

* ``CharDescendingOrderEnumerationListStrategy``
* ``CharAscendingOrderEnumerationListStrategy``
* ``IntegerAscendingOrderEnumerationListStrategy``
* ``IntegerDescendingOrderEnumerationListStrategy``

```java
new EnvironmentConfigurationBuilder()
                .listEnumeration()
                    .withEnumerationListStrategy(enumerationListStrategy)
                .and().build();
```

### ``value()``

```java
new EnvironmentConfigurationBuilder()
                .value()
                    .withMathContext(MathContext.DECIMAL128)
                    .withConverters(converters)
                    .withEqualComparator(equalComparator)
                    .withLowerComparator(lowerComparator)
                    .withGreaterComparator(greaterComparator)
                    .withIdenticalComparator(identicalComparator)
                    .withMapSelectionExtractor(mapSelectionExtractor)
                    .withTypeExtractor(typeExtractor)
                .and().build();
```

<p style="text-align: justify;">
The <code>value()</code> method returns an instance of <code>AndValueConfigurationBuilder</code> allowing to configure Jtwig value handling.
</p>

* ``MathContext`` sets the java BigDecimal Math Context, note that Jtwig converts all numbers to BigDecimal.
* ``Converters`` allows one to convert values between different types. This might be used for operations, functions and tags (loops, for example).
* ``EqualComparator`` (``==``), ``LowerComparator`` (``<``), ``GreaterComparator`` (``>``), ``IdenticalComparator`` (``===``) are used when comparing two values.
* ``MapSelectionExtractor`` extracts a value given a key, is used in expressions lile ``variable['key']``.
* ``TypeExtractor`` allows one to retrieve the type from a given value.


### ``withExtension(Extension)``

<p style="text-align: justify;">
In order to add extensions to the Jtwig core behaviour one can use the <code>withExtension</code> method. Currently available extensions will be explained further on.
</p>
