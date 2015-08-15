# `embed` construct

<p style="text-align: justify;">
The embed construct works like a multiple inheritance mechanism, allowing developers to include and extend parent templates in one go.
</p>

```twig
{% embed resourceExpression ignore missing with mapExpression only %}
  {% block blockId %}
    ... redefine template ...
  {% endblock %}
{% endembed %}
```

<p style="text-align: justify;">
Functionality wise, this construct is the result of merging the <code>include</code> feature with the <code>extends</code> one.
</p>

> Inside an <code>embed</code> tag one can only specify <code>block</code> tags which will override the parent template included.

### Arguments

<p style="text-align: justify;">
The <code>embed</code> arguments are exactly the same as the <code>include</code> construct and have identical behaviour.
</p>