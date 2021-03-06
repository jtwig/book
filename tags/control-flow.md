# Control Flow constructs

<p style="text-align: justify;">
Jtwig implements basic control flow constructs such as <code>if</code> conditions and <code>for</code> loops with the exact same syntax as Twig.
</p>

## `if` conditions

<p style="text-align: justify;">
If conditions are the simpliest control flow in Jtwig. It supports consecutive <code>elseif</code> conditions and the common <code>else</code> construct too.
</p>


```twig
{% if (expression) %}
  ... content if expression is evaluated to true ...
{% elseif (anotherExpression) %}
  ... content if anotherExpression is evaluated to true ...    
{% else %}
  ... content if none of the previous conditions are met ...
{% endif %}
```
    
<p style="text-align: justify;">
Note that if constructs will only output the content of the first block which condition is evaluated to true. The way Jtwig evaluates an expression to true is configurable and will be explained further on this manual.
</p>

<p style="text-align: justify;">
In terms of variable scoping, if inner content shares the context with the parent context, this means if conditions can affect variables in the outer scope.
</p>

```twig
{% set variable = "a" %}
{% if (true) %}
  {% set variable = "b" %}
{% endif %}
{{ variable }}
```

<p style="text-align: justify;">
The previous example will output <code>b</code> which illustrates how scoping works on if conditions by sharing the context with the parent construct.
</p>

## `for` loops

<p style="text-align: justify;">
Again based on Twig, Jtwig also implements, in a similar fashion <code>for</code> loops. It allows one to iterate over a list or a map. In this specific a list must be seens as a map where the key is the index.
</p>

```twig
{# Example with list #}
{% for item in list %}
  ... content using variable item ...
{% endfor %}

{# Example with map #}
{% for key, value in map %}
  ... content using variables key and value ...
{% endfor %}
```

<p style="text-align: justify;">
Similar to the boolean expression evaluation, list or map evaluation in Jtwig is also configurable and will be discussed further on in this manual.
</p>

### `loop` variable

<p style="text-align: justify;">
For loops come with an extra variable defined in the context, the <code>loop</code> variable. The loop variable provides a set of useful properties when within a for loop, check below the properties exposed by this variable.
</p>

| Property | Description |
|----------|-------------|
| `length` | Size of the list or map being iterated |
| `index`  | Current iteration count starting in 1 |
| `index0` | Current iteration count starting in 0 |
| `revindex` | Remaining number of iterations to reach the end of the list or map, ends in 1 |
| `revindex0` | Remaining number of iterations to reach the end of the list or map, ends in 0 |
| `first` | Boolean property only true in the first iteration |
| `last` | Boolean property only true in the last iteration |
| `parent` | Accessing the parent context |

```twig
{% for item in [1, 2, 3] %}
  {% if (loop.first) %}
     Start
  {% endif %}
{% endfor %}
```

<p style="text-align: justify;">
The previous example will output <code>Start</code> only once.
This <code>loop</code> variable is only bound to the for context, it means this variable will not be visible outside of the for loop scope. 
If there is a <code>loop</code> variable in the context, it will not be overriden but to access it one need to get the parent context, for example:
</p>

```twig
{% set loop = 1 %}
{% for item in [1, 2, 3] %}
  {% if (loop.first) %}
     {{ loop.parent.loop }}
     {% set loop = 2 %}
  {% endif %}
{% endfor %}
{{ loop }}
```
<p style="text-align: justify;">
The previous template will print <code>1 2</code>. Note that setting <code>loop</code> inside the for loop will write to the context, but won't override the for loop bound variable.
</p>