# Built-in Functions

### ``escape``

<p style="text-align: justify;">
The <code>escape</code> function allows to set the escape mode of the current context. A escape mode can be provided in order to choose which escaping strategy to use. If <code>false</code> is provided, it will set the escape mode to none.
</p>

```
escape(<Value> [, <Escape Mode>])
```

<p style="text-align: justify;">
By default it uses HTML escape mode, meaning HTML special characters will be then escaped. Escape modes were already described in Tags > Other Tags > <code>autoescape</code> tag.
</p>

```twig
{% autoescape 'html' %}
& {{ '&' | escape(false) }}
{%.endautoescape %}
```

<p style="text-align: justify;">
The previous example, based on the Jtwig implementation of its processing pipeline and the escape mode functionality will produce <code>&amp;&</code>.
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


### ``batch``

<p style="text-align: justify;">
The batch function splits a given list in equally sized groups of items. It expects two or three arguments. A list as first argument, note that a list in Jtwig is a configurable concept as mentioned previously, it depends on the converter defined in the environment. The second argument is the group size. There is also an optional third argument used as padding, that is, if the last group is incomplete, the third argument will be used to fill it. 
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