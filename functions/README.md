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
{%. autoescape 'HTML' %}
{{. '&' | raw }}
{%. endautoescape %}
```

<p style="text-align: justify;">
The previous example will produce <code>&</code> as output.
</p>