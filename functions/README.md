# Built-in Functions


### ``abs``

<p style="text-align: justify;">
Mathematical function allowing to get the absolute value of an expression. For example, <code>{{ '{{' }} abs(-1) {{ '}}' }}</code> would produce <code>1</code>. It is expecting only one argument which must be converted to a number. Such conversion uses the <code>NumberConverter</code> configured. For more details check the Environment documentation.
</p>

### ``batch``

<p style="text-align: justify;">
The batch function splits a given list in equally sized groups of items. It expects two or three arguments. A list as first argument, note that a list in Jtwig is a configurable concept as mentioned previously, whereby the ``CollectionConverter`` defined in the configuration will be used, it depends on the converter defined in the environment. The second argument is the group size. There is also an optional third argument used as padding, that is, if the last group is incomplete, the third argument will be used to fill it. 
</p>


```twig
{{ batch([1,2,3], 2) }}
```

<p style="text-align: justify;">
The previous example will output <code>[[1, 2], [3]]</code>.
</p>


```twig
{{ batch([1,2,3], 2, 0) }}
```


<p style="text-align: justify;">
The previous example, now with the padding argument, will output <code>[[1, 2], [3, 0]]</code>.
</p>

### ``block``

<p style="text-align: justify;">
Block function can be used to output the content of a defined block tag (check <code>{{ '{% block %}' }}</code> tag definition).
</p>

```twig
{% block one %}Hello{% block %}{{ block('one') }}
```

<p style="text-align: justify;">
The previous example will print <code>HelloHello</code>.
</p>

### ``capitalize``

<p style="text-align: justify;">
The capitalize function is expecting one argument. It converts that argument to a String, using the <code>StringConverter</code> (check <code>Environment</code> documentation for more information).
</p>

```twig
{{ capitalize('hello world') }}
```

<p style="text-align: justify;">
The previous template will render as <code>Hello world</code> which is the result of capilatizing the first word.
</p>

### ``concat`` or ``concatenate``

<p style="text-align: justify;">
This function allows one to concatenate a set of strings. It is expecting an arbitrary number of arguments (varargs).
</p>

```twig
{{ concat('1', '+', '1', '=', '2') }}
```

<p style="text-align: justify;">
Under the wood it uses the defined ``StringConverter`` to convert individual objects to a string representation and then concatenating them. The previous example will output ``1+1=2``.
</p>

### ``constant``

<p style="text-align: justify;">
The constant function comes with two possible outputs depending on the number of arguments supplied. If one argument is supplied, it will return the value of the constant. If two arguments are provided, then it will compare the constant value against the second argument.
</p>

```twig
{{ constant("org.jtwig.example.TestClass.CONSTANT_NAME") }}
```

<p style="text-align: justify;">
As shown in the above example, the expression will print the result of evaluating (using reflection) the constant with name <code>CONSTANT_NAME</code> defined in class <code>org.jtwig.example.TestClass</code>. Note that the evaluation will only work if the constant is public.
</p>

```twig
{{ constant("org.jtwig.example.TestClass.CONSTANT_NAME", "value") }}
```

<p style="text-align: justify;">
The above example will return a Boolean expression. It will be <code>true</code> if the constant value is equal to <code>"value"</code>.
</p>

### ``default``

<p style="text-align: justify;">
The default function is expecting two arguments. It returns the second argument if the first argument is either <code>null</code> or <code>Undefined</code>.
</p>

```twig
{{ default(null, 'Hello') }} {{ default(undefinedVariable, 'World') }}
```

<p style="text-align: justify;">
if variable <code>undefinedVariable</code> is not defined in the provided <code>JtwigModel</code> then the previous example will produce <code>Hello World</code>.
</p>

### ``defined``

<p style="text-align: justify;">
The defined function is useful to check if a given expression is defined or not. This logic is tied to the definition of an <code>Undefined</code> expression, explained later on (Jtwig core engine). It returns <code>true</code> if the given expression is defined, <code>false</code> otherwise.
</p>

```twig
{% if (defined([1, 2][5])) %}KO{% else %}OK{% endif %}
```

<p style="text-align: justify;">
The previous example will output <code>OK</code> because index <code>5</code> of list <code>[1, 2]</code> is undefined.
</p>

### ``empty``

<p style="text-align: justify;">
The empty function returns a boolean value. As input it is expecting a generic object, it returns true if the given input falls in one of the following scenarios:
</p>

* ``null``
* ``Undefined``
* non-empty list (implementing ``Iterable`` interface) of items
* non-empty array
* non-empty map
* non-zero number

<p style="text-align: justify;">
Note that under the wood this function is using <code>NumberConverter</code> and <code>CollectionConveter</code>. Check the example below.
</p>

```twig
{% if (empty([1, 2])) %}A{% else %}B{% endif %}
```

<p style="text-align: justify;">
The previous example produces <code>B</code>.
</p>

### ``escape``

<p style="text-align: justify;">
The <code>escape</code> function allows to set the escape mode of the current context. A escape mode can be provided in order to choose which escaping strategy to use. If <code>false</code> is provided, it will set the escape mode to none.
</p>

```
escape(<Value> [, <Escape Mode>])
```

<p style="text-align: justify;">
By default it uses HTML escape mode, meaning HTML special characters will be then escaped. For more information about available escaping strategies check <code>Environment</code> chapter.
</p>

```twig
{% autoescape 'html' %}
& {{ '&' | escape(false) }}
{%.endautoescape %}
```

<p style="text-align: justify;">
The previous example, based on the Jtwig implementation of its processing pipeline and the escape mode functionality will produce <code>&amp;&</code>.
</p>

### ``even``

<p style="text-align: justify;">
This function is quite simple, it is expecting one number as argument and it returns true when that number is even, false otherwise.
</p>


```twig
{% if (even(2)) %}A{% else %}B{% endif %}
```

<p style="text-align: justify;">
The previous example prints <code>A</code>. Note that the even function uses the <code>NumberConverter</code> concept to try to conver the given input to a number. If this conversion fails an exception will be thrown.
</p>

### ``first``

<p style="text-align: justify;">
The first function returns the first element of a collection or String. If the argument provided is not a collection or a String, it will just return the input argument.
</p>

```twig
{{ first([1, 2]) }}
```

<p style="text-align: justify;">
If the given argument is an empty list or String, then it returns <code>Undefined</code>. Note that this function uses the <code>CollectionConverter</code> mechanism. The previous template will output <code>1</code>.
</p>

### ``format``

<p style="text-align: justify;">
The format function is just a Jtwig wrapper to call the <code>String.format</code> method available in Java. It receives an arbitrary number of arguments where the first is the template parameter (converted to a String) and the remaining arguments is provided as the model values for the <code>String.format</code> method.
</p>


```twig
{{ format('hello %s', 'world') }}
```

<p style="text-align: justify;">
The previous example will print <code>hello world</code>. Note that this function uses the <code>StringConverter</code> (check <code>Environment</code> documentation for more information).
</p>

### ``iterable``

<p style="text-align: justify;">
The iterable function allows one to check if a given argument is a collection for loops can iterate over, or index/map selections can be used.
</p>

```twig
{% if (iterable(2)) %}A{% else %}B{% endif %}
```

<p style="text-align: justify;">
Iterable uses under the wood the <code>CollectionConverter</code>, which whenever an object can be converted to a Jtwig collection it will be iterable. The previous template will render <code>B</code> because <code>2</code> is not iterable as per default configuration.
</p>

### ``join``

<p style="text-align: justify;">
The <code>join</code> function provides functionality somehow similar to the <code>concat</code> function, however they have some differences. To start with, <code>join</code> takes only one or two arguments, where the first argument is expected to be a list and the second, optional, argument a string to be used as the separator.
</p>

```twig
{{ join([1, null, 2], ', ') }}
```

<p style="text-align: justify;">
The previous example will print <code>1, 2</code>. Note that, <code>join</code> function ignores <code>null</code> values.
</p>

### ``keys``

<p style="text-align: justify;">
Keys function can be used to expose the collection of keys for a given collection. It uses the configured <code>CollectionConverter</code> (for more details check the Environment documentation).
</p>

```twig
{{ keys(['A', 'B']) }}
```

<p style="text-align: justify;">
The previous example, as per the default configuration, will print <code>[1, 2]</code>.
</p>

### ``last``

<p style="text-align: justify;">
The last function returns the last element of a collection or String. If the argument provided is not a collection or a String, it will just return the input argument.
</p>

```twig
{{ last([1, 2]) }}
```

<p style="text-align: justify;">
If the given argument is an empty list or String, then it returns <code>Undefined</code>. Note that this function uses the <code>CollectionConverter</code> mechanism (check <code>Environment</code> documentation for more information). The previous template will output <code>2</code>.
</p>

### ``length``

<p style="text-align: justify;">
The length function returns the length of a given collection or String. If neither a collection or String is provided then it returns <code>0</code> for both <code>null</code> and <code>Undefined</code>, otherwise <code>1</code> will be the result.
</p>

```twig
{{ length([1, 2]) }}
```

```twig
{{ length(null) }}
```

```twig
{{ length(9) }}
```

<p style="text-align: justify;">
The previous examples will print respectively <code>2</code>, <code>0</code> and <code>1</code>. Note that this function uses the defined <code>CollectionConverter</code> configured, for more information visit the <code>Environment</code> documentation.
</p>

### ``lower``

<p style="text-align: justify;">
Lowers the case of the String provided. Note that this function uses the <code>StringConverter</code> (check <code>Environment</code> documentation for more information). The following example will produce <code>jtwig</code>.
</p>

```twig
{{ lower('JTWIG') }}
```

### ``merge``

<p style="text-align: justify;">
The <code>merge</code> function allows one to merge an arbitrary number of lists together by the given order. This function requires at least two arguments to run. It also supports singular elements as arguments.
</p>

```twig
{{ merge(1, 2, 3) }}
```

```twig
{{ merge([1, 2], 3) }}
```

<p style="text-align: justify;">
The previous two examples return the same output, which is, <code>[1, 2, 3]</code>. Note that, this function uses the <code>CollectionConverter</code> defined by the Jtwig configuration.
</p>

### ``nl2br``

<p style="text-align: justify;">
This function allows one to convert new line characters into it's HTML sibling <code>&lt;br /&gt;</code>, just as simple as that. It uses <code>StringConverter</code> (check <code>Environment</code> documentation for more information) to convert the given argument to a String.
</p>

### ``number_format``

<p style="text-align: justify;">
The <code>number_format</code> allows one to format a given number with specific symbols for the grouping and decimal separators, also the number of fractional digits. This function expects at least one argument and can receive up to four arguments. The list of arguments is presented below by the order they are expected by Jtwig.
</p>

1. The number to be formatted
2. The number of fractional digits (optional)
3. The decimal separator (optional)
4. The grouping separator (optional)

```twig
{{ number_format(11000.136, 2, '.', ' ') }}
```

<p style="text-align: justify;">
The previous example will produce <code>11 000.14</code>. The rounding applied in here is the same strategy as <code>BigDecimal.ROUND_HALF_DOWN</code> (check Java documentation for more information). This function uses <code>StringConverter</code> to convert the third and fourth arguments to Strings, it also uses the <code>NumberConverter</code> to convert the first and second arguments to numbers, check <code>Environment</code> documentation for more information about this converters.
</p>

### ``odd``

<p style="text-align: justify;">
This is the oposite of the <code>even</code> function, it is expecting one number as argument and it returns true when that number is odd, false otherwise.
</p>


```twig
{% if (odd(2)) %}A{% else %}B{% endif %}
```

<p style="text-align: justify;">
The previous example prints <code>B</code>. Note that the even function uses the <code>NumberConverter</code> concept to try to conver the given input to a number. If this conversion fails an exception will be thrown.
</p>

### ``raw``

<p style="text-align: justify;">
This function clears the current escape mode of the context. It is equivalent to <code>escape(false)</code>. This function does not take arguments. 
</p>

```twig
{% autoescape 'HTML' %}
{{ '&' | raw }}
{% endautoescape %}
```

<p style="text-align: justify;">
The previous example will produce <code>&</code> as output.
</p> 

### ``replace``

<p style="text-align: justify;">
The replace function allows one to specify a String and a map of replacements replacing all the ocurrences of the keys in the provided map by their respective value converted to a String. It expects two arguments, where it uses <code>StringConverter</code> to convert the first argument to a String and <code>CollectionConverter</code> to convert the second argument to a list of key value pairs.
</p>


```twig
{{ replace('Hello %name%', { '%name%': 'world' }) }}
```

<p style="text-align: justify;">
The previous example will produce <code>Hello world</code> as output.
</p>

### ``reverse``

<p style="text-align: justify;">
Reverse function reverses the order of the elements in a given collection or String. If no collection neither String is provided then it returns the given argument.
</p>

```twig
{{ reverse([1, 2]) }}
```

<p style="text-align: justify;">
The previous example will print <code>[2, 1]</code>. Note that this function uses the defined <code>CollectionConverter</code> configured, for more information visit the <code>Environment</code> documentation.
</p>

### ``round``

<p style="text-align: justify;">
The round function allows one to round a given number to integer. An optional strategy can be specified as second argument:
</p>

* ``'CEIL'``
* ``'FLOOR'``


```twig
{{ round(1.3, 'CEIL') }}
```

<p style="text-align: justify;">
The previous example will produce <code>2</code>. Note that the strategy selection is case insensitive, so one can either specify <code>'CEIL'</code> or <code>'ceil'</code>. If the second argument is not specified <code>BigDecimal.ROUND_HALF_DOWN</code> will be applied. For further information check the official Java documentation.
</p>

### ``slice``

<p style="text-align: justify;">
This function is expecting three arguments, where the first argument can either be a String or a collection (it uses <code>CollectionConverter</code> under the wood), and an integer as second and third arguments.
</p>

```twig
{{ slice("123", 1, 1) }}
```

```twig
{{ slice([1, 2, 3], 0, 2) }}
```

<p style="text-align: justify;">
The second argument is the index position the slice will start from (inclusive), where the third argument is the length of the slice. As shown in the previous two examples, the result will be <code>"2"</code> and <code>[1, 2]</code> respectively. Note that, slice is smart enough to handle boudary cases, for exaple:
</p>

```twig
{{ slice("123", 2, 3) }}
```

```twig
{{ slice("123", 5, 1) }}
```

<p style="text-align: justify;">
The previous examples will still return a slice, depending on the number of characters or items provided in the first argument, the previous examples would then resolve the slice to <code>"3"</code> and <code>""</code>
</p>

### ``sort``

<p style="text-align: justify;">
Sort can be used to sort elements of a given collection in ascending order. It is based on the underlying core Java <code>java.lang.Comparable</code> interface, which elements should implement.
</p>

```twig
{{ sort([1, 3, 2]) }}
```

<p style="text-align: justify;">
The previous example will produce <code>[1, 2, 3]</code>.
</p>

### ``split``

<p style="text-align: justify;">
This function expects two arguments, using the second argument provided to split the first one into a collection. Such arguments are converted to String using the <code>StringConverter</code> configured in the <code>Environment</code> as detailed previously.
</p>

```twig
{{ split('jtwig-2', '-') }}
```

<p style="text-align: justify;">
The previous example will return <code>[jtwig, 2]</code>.
</p>

### ``striptags``

<p style="text-align: justify;">
The <code>striptags</code> function is expecting at least one argument or two at most. This function emulates the PHP <code>strip_tags</code> function behaviour in Java. The first argument is the String which HTML elements will be stripped. Where the second optional argument (a String aswell) enables users to specify a list of allowed tags (tags that won't be stripped). 
</p>

```twig
{{ striptags('<a>jtwig</a><button>Submit</button>', '<a>') }}
```

<p style="text-align: justify;">
The previous example will produce <code>&lt;a&gt;jtwig&lt;/a&gt;Submit</code>. Note that this function uses <code>StringConverter</code> to convert the arguments to a String, check <code>Environment</code> documentation for further information.
</p>

### ``title``

<p style="text-align: justify;">
The title function is expecting one String argument, capitalizing the first letter of all words present in it.
</p>

```twig
{{ title('hello world') }}
```

<p style="text-align: justify;">
The previous example will produce <code>Hello World</code>. Note that this function uses <code>StringConverter</code> to convert the arguments to a String, check <code>Environment</code> documentation for further information.
</p>

### ``trim``

<p style="text-align: justify;">
Similar to the Java sibling <code>String::trim</code>, the trim function in Jtwig removes any whitespace characters from the beggining and/or ending of the given argument.
</p>


```twig
{{ trim('  Hello World  ') }}
```

<p style="text-align: justify;">
The previous example will produce <code>Hello World</code>. Note that this function uses <code>StringConverter</code> to convert the arguments to a String, check <code>Environment</code> documentation for further information.
</p>

### ``upper``

<p style="text-align: justify;">
Changes the case of the String provided by turning all into capitals. Note that this function uses the <code>StringConverter</code> (check <code>Environment</code> documentation for more information). The following example will produce <code>JTWIG</code>.
</p>


```twig
{{ upper('jtwig') }}
```

### ``url_encode``

<p style="text-align: justify;">
Encoding values to a url is the role of this function. It is expecting either a String or a map.
</p>

```twig
{{ url_encode({id: 1, special: '&'}) }}
```

<p style="text-align: justify;">
The previous example produces <code>id=1&amp;special=%26</code>.
</p>

```twig
{{ url_encode('one&two') }}
```

<p style="text-align: justify;">
The previous example produces <code>one%26two</code>.
</p>
