# Other Tags


## `autoescape`

<p style="text-align: justify;">
The <code>autoescape</code> construct only change the escape mode which will be used by the processing pipeline to generate the output. The escaping modes currently available are:
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
The escaping functionality is attached to the very end of the rendering pipeline as explained in Jtwig Core > Rendering pipeline.
</p>

## `filter`

<p style="text-align: justify;">
The filter construct is the way apply functions the a given content. It uses the provided body as the first argument in the specified function.
</p>

```twig
{% filter lower | capitalize %}
HELLO WORLD
{% endfilter %}
```

<p style="text-align: justify;">
The previous example will produce <code>Hello world</code>. As we can see, the filter specified results in the composition of two distinct functions, it will first apply the <code>lower</code> function to the content <code>HELLO WORLD</code>, producing <code>hello world</code> and then apply the <code>capitalize</code> function producing <code>Hello world</code>.
</p>

## `verbatim`

<p style="text-align: justify;">
The <code>verbatim</code> tag is usefull avoiding the specifics around Jtwig syntax, as it will not try to parse the content.
</p>

```twig
{% verbatim %}
{{ test }}
{% endverbatim %}
```

<p style="text-align: justify;">
The output of the previous template will be <code>{{ '{{ test }}' }}</code>.
</p>