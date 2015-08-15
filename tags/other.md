# Other Tags

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