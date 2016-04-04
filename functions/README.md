# Built-in Functions

### ``escape``

<p style="text-align: justify;">
The <code>escape</code> function allows to escape a given value. A escape mode can be provided in order to choose which escaping strategy to perform.
</p>

```twig
escape(<Value> [, <Escape Mode>])
```

<p style="text-align: justify;">
By default it uses HTML escape mode, meaning HTML special characters will be then escaped. Escape modes were already described in Tags > Commands > Autoescape tag.
</p>

### ``raw``

<p style="text-align: justify;">
This function clears the current escape mode set for a given context.
</p>