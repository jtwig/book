# Other Tags


## `autoescape`

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
The escaping functionality is attached to the very end of the rendering pipeline as explained in Jtwig Core > Rendering pipeline.
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