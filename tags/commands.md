# Command constructs

<p style="text-align: justify;">
Command constructs allows one to run specific commands against Jtwig. An important aspect common to all commands is that they never produce content, they only act as a side effect tool.
</p>

## `set` command

<p style="text-align: justify;">
The set command allows to specify an assignment operation inside a Jtwig template, it will assign to the result of an expression to the specified variable.
</p>

```twig
{% set var = 2 + 3 %}
```

<p style="text-align: justify;">
In the previous example one assigned the result of evaluating the expression <code>2 + 3</code> to the variable <code>var</code>. Note again that the output of the previous example will be empty because, as mentioned before, <code>set</code> as a command, does not produce content, it just affects the context defining, or redefining a variable.
</p>

## `do` command

<p style="text-align: justify;">
The <code>do</code> command just evaluates a given expression.
</p>

```twig
{% do something.run() %}
```

<p style="text-align: justify;">
There is not a lot to say about this construct, it might be usefull to trigger behaviour from the template by running a Java method for example.
</p>

## `flush` command

<p style="text-align: justify;">
A common operation over streams is the <code>flush</code> operation. As a template engine Jtwig is very much associated with output buffers, which can be explicitly flushed. This forces the buffer to be written, for example, in a web application it will force the data to be sent from the ouput buffer to the destination over the wire.
</p>

```twig
{% flush %}
```


## `autoescape` construct

<p style="text-align: justify;">
The <code>autoescape</code> construct allows one to set the escape mode to the given content. The escaping modes currently available are:
</p>

* `false` - No escaping at all
* `'js'` or `'javascript'` - Javascript escaping mode
* `html` - Escaping special HTML characters

```twig
{% autoescape 'html' %}
<a href="#">Link</a>
{% endautoescape %}
```

<p style="text-align: justify;">
Later on one will describe how does the escaping functionality works behind the scenes.
</p>
