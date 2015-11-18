# `extends` construct

<p style="text-align: justify;">
The extends construct allows one to extend a given template redefining some of it's blocks. The concept of extending is very much associated with the concept of block detailed below. The extends construct expects one argument, a path for another Jtwig template.
</p>

```twig
{% extends pathExpression %}
```

### Path

<p style="text-align: justify;">
The path can be any expression that, once evaluated will then be used by the resource resolution mechanism in order to retrieve another Jtwig template. This resolution mechanism will be detailed futher on.
</p>

<p style="text-align: justify;">
The extends template can then be followed by a sequence of <code>set</code>, <code>block</code> or <code>import</code> constructs only. For example:
</p>

```twig
{% extends pathExpression %}
{% import pathExpression as importAlias %}
{% set var = 1 %}
{% block ... %}{% endblock %}
```