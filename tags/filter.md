# `filter` construct

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