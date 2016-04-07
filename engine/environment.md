
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
However, as shown in the previous example, the <code>DefaultEnvironmentConfiguration</code> creates an immutable <code>EnvironmentConfiguration</code> instance. To overcome that limitation and customize Jtwig configuration the <code>EnvironmentConfigurationBuilder</code> API was created. It comes with a set of methods to specify all possible Jtwig behaviour. As Jtwig is highly configurable, this API offers a tree of builders to organise and ease the specification of customised behaviour. Note that all the builders follow a common convention:
</p>

* All the builder methods starting with ``with``  will set the underlying configuration field.
* All methods starting with ``without`` will unset the underlying configuration field.
* ``add`` methods will append elements to the current list or map of values. For example, Jtwig allows the user to specify multiple extensions, in this case, ``add`` can be used to add another extension on top already existing ones.
* ``set`` methods will override the currently defined list or maps of values.
* ``filter`` methods allows the user to specify a filtering predicate which will be used to filter the existing list or map of items, such methods are useful to modify pre-defined behaviour.
* ``and`` methods enables developers to return the parent builder.

### Extending the default configuration

<p style="text-align: justify;">
An useful constructor of this builder is the prototype constructor which allows one to initialize the builder given an instance of an EnvironmentConfiguration. Specially useful when extending the default configuration (the most common scenario), instead of creating an entire new one.
</p>

```java
new EnvironmentConfigurationBuilder(new DefaultEnvironmentConfiguration())
                .build()
```

<p style="text-align: justify;">
The example above will create an instance of EnvironmentConfiguration copying all the definitions from the default configuration. One can then use the builder to modify the default configuration. Another way to achieve the same is by using the static method <code>EnvironmentConfigurationBuilder::configuration</code>, which makes the previous code snippet equivalent to the following one.
</p>

```java
EnvironmentConfigurationBuilder.configuration().build()
```

### ``parser()``

<p style="text-align: justify;">
The <code>parser()</code> method returns an instance of <code>AndJtwigParserConfigurationBuilder</code>, such class was built for the purpose of configuring the Jtwig parser. Let's see an example of it.
</p>

```java
EnvironmentConfiguration configuration = EnvironmentConfigurationBuilder
                .configuration()
                    .parser()
                        .syntax()
                            .withStartCode("{%").withEndCode("%}")
                            .withStartOutput("{{").withEndOutput("}}")
                            .withStartComment("{#").withEndComment("#}")
                        .and()
                        .addonParserProviders().add(customAddonParser()).and()
                        .binaryOperators().add(customBinaryOperator()).and()
                        .unaryOperators().add(customUnaryOperator()).and()
                        .withoutTemplateCache()
                    .and()
                .build();
```

<p style="text-align: justify;">
With this one can specify:
</p>

* ``StartCode``, ``EndCode``, ``StartOutput``, ``EndOutput``, ``StartComment`` and ``EndComment`` allows one customize the syntactic symbols used by Jtwig code islands.
* ``AddonParserProviders``, ``BinaryOperators`` and ``UnaryOperators`` provides API to enhance the parser with extra addons, this will be detailed further on. All the mentioned methods are used to build lists of objects which means one can specify as many as we want.
* ``TemplateCache`` setting gives the user the possibility to configure a cache for compiled Jtwig templates. Such mechanism speeds up the parsing operation. It uses **Resource** as key and returns, as mentioned, the Jtwig compiled templates. By caching it, operations like reading files and flatening the template structure can get a significant performance boost. Jtwig core comes with one implementation used by default: ``InMemoryConcurrentPersistentTemplateCache`` which was built with high performance standards.

### ``functions()``

<p style="text-align: justify;">
The <code>functions()</code> method returns a configurable list builder of Jtwig functions. Such functions will be provided to the Jtwig function repository mechanism, a fundamental piece of the function resolution system.
</p>

```java
EnvironmentConfiguration configuration = EnvironmentConfigurationBuilder
                .configuration()
                    .functions()
                        .add(jtwigFunction)
                    .and()
                .build();
```

### ``resources()``

<p style="text-align: justify;">
The <code>resources()</code> method returns an instance of <code>AndResourceResolverConfigurationBuilder</code> used to build the resource resolver.
</p>

```java
EnvironmentConfiguration configuration = EnvironmentConfigurationBuilder
                .configuration()
                    .resources()
                        .resourceResolvers().add(resourceResolver).and()
                    .and()
                .build();
```

<p style="text-align: justify;">
It's possible to specify multiple resources resolvers. Resource resolvers are detailed further on. A default input charset can also be provided, it will be used as the default input encoding for loaded resources. To understand what encoding gets used, the specific implementation of resource resolver must be analysed.
</p>

### ``render()``

<p style="text-align: justify;">
The <code>render()</code> method returns an instance of <code>AndRenderConfigurationBuilder</code> which provides a set of useful builder methods to configure the rendering, let's check the following example.
</p>

```java
EnvironmentConfiguration result = EnvironmentConfigurationBuilder
                .configuration()
                    .render()
                        .withStrictMode(strictMode)
                        .withInitialEscapeMode(initialEscapeMode)
                        .withOutputCharset(outputCharset)
                        .nodeRenders().add(CustomNode.class, nodeRender).and()
                        .expressionCalculators()
                            .add(CustomExpression.class, expCalculator).and()
                        .binaryExpressionCalculators()
                            .add(CustomBinaryOperator.class, binOpCalc).and()
                        .unaryExpressionCalculators()
                            .add(CustomUnaryOperator.class, unaryOpCalc).and()
                        .testExpressionCalculators()
                            .add(CustomTestExpression.class, testCalc).and()
                    .and()
                .build();
```

<p style="text-align: justify;">
Here you can find the following properties:
</p>

* ``StrictMode`` sets the way to resolve variables in Jtwig, if strict mode is active, undefined variables will throw an exception when evaluated. However, if strict mode is disabled, it will be evaluated to ``Undefined.UNDEFINED``. Strict mode is disabled by default.
* ``InitialEscapeMode`` as the name says sets the initial escape mode, which by default is set to ``NONE``, which means, strings wont be escaped when rendering the template. Escape modes were already mentioned before (Tags > Commands).
* ``OutputChatset`` defines the default output charset for Jtwig, this is used at the Jtwig rendering stage.
* ``NodeRenders`` is a map of Content Node type to an implementation of the RenderNode interface. Such interface tell Jtwig how to render such type of element once they appear on the Jtwig rendering tree.
* ``ExpressionCalculators`` holds the mapping from Expression to it's calculator, allowing Jtwig to evaluate the given expression value.
* ``BinaryExpressionCalculators``, ``UnaryExpressionCalculators`` and ``TestExpressionCalculators`` again, allows the user to specify implementations of calculators so that Jtwig can use to evaluate such expressions value.

### ``propertyResolvers()``

<p style="text-align: justify;">
This method allows one to setup multiple property resolvers. The default property resolution mechanism was already detailed when describing the selection operator behaviour.
</p>

```java
EnvironmentConfiguration configuration = EnvironmentConfigurationBuilder
                .configuration()
                    .propertyResolver()
                        .add(propertyResolver)
                    .and()
                .build();
```

### ``enumerationStrategies()``

<p style="text-align: justify;">
The <code>enumerationStrategies()</code> method allows to configure the list enumeration stretagies. This strategies are used when resolving lists by comprehension in Jtwig. By default, and as mentioned before, Jtwig comes with four different strategies:
</p>

* ``CharDescendingOrderEnumerationListStrategy``
* ``CharAscendingOrderEnumerationListStrategy``
* ``IntegerAscendingOrderEnumerationListStrategy``
* ``IntegerDescendingOrderEnumerationListStrategy``

```java
EnvironmentConfiguration configuration = EnvironmentConfigurationBuilder
                .configuration()
                    .enumerationStrategies()
                        .add(enumerationListStrategy)
                    .and()
                .build();
```

### ``value()``

```java
EnvironmentConfiguration configuration = EnvironmentConfigurationBuilder
                .configuration()
                    .value()
                        .withMathContext(mathContext)
                        .withRoundingMode(roundingMode)
                        .withValueComparator(valueComparator)
                        .withStringConverter(stringConverter)
                        .numberConverters().add(numberConverter).and()
                        .booleanConverters().add(booleanConverter).and()
                        .charConverters().add(charConverter).and()
                        .collectionConverters().add(collectionConverter).and()
                    .and()
                .build();
```

<p style="text-align: justify;">
The <code>value()</code> method returns an instance of <code>AndValueConfigurationBuilder</code> allowing to configure Jtwig value handling.
</p>

* ``MathContext`` sets the java BigDecimal Math Context, note that Jtwig converts all numbers to BigDecimal.
* ``RoundingMode`` is used by mathematical operations like divide and multiply as rounding might be applied.
* ``ValueComparator`` is used for all comparisons in Jtwig. By default, the value comparator tries to convert the operands to a number (then comparing using the BigDecimal equals method) or it converts the operands to a string (using the String equals method).
* ``StringConverter`` allows to specify the logic to use when converting objects to a String value, note this is used to serialize any object in Jtwig, the default implementation is null safe (returning empty string if null) and only returns the result of the Java native Object ``toString`` method.
* ``NumberConverter``, ``BooleanConverter``, ``CharConverter`` and ``CollectionConverter`` allows Jtwig to extract such types of values from a generic Java object.

### ``extensions()``

<p style="text-align: justify;">
In order to add extensions to the Jtwig core behaviour one can use the <code>withExtension</code> method. Note that by default Jtwig Core does have any extension, however as part of the Jtwig community there is a list of already created extensions.
</p>

```java
EnvironmentConfiguration configuration = EnvironmentConfigurationBuilder
                .configuration()
                    .extensions()
                        .add(customExtension1)
                        .add(customExtension2)
                    .and()
                .build();
```


### ``parameters()``

<p style="text-align: justify;">
In a more advanced context, Jtwig allows developers to add custom configuration parameters. This can be used by extensions further on, during rendering time from the ``Environment::parameter(String)`` method.
</p>


```java
EnvironmentConfiguration configuration = EnvironmentConfigurationBuilder
                .configuration()
                    .parameters()
                        .add(parameter1, value1)
                        .add(parameter2, value2)
                    .and()
                .build();
```