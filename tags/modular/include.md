# `include` construct

<p style="text-align: justify;">
The simpliest modular construct in Jtwig is the <code>include</code> construct. By using this construct one can include another template.
</p>

```twig
{% include 'template.twig' ignore missing with {} only %}
```

<p style="text-align: justify;">
The previous example shows all <code>include</code> possible arguments. In this section one will describe all arguments in detail.
</p>

## Path (mandatory)

<p style="text-align: justify;">
In it's simple form <code>include</code> only requires one argument, the template path. This is an expression which will be evaluated and used as the path for the Jtwig template to include.
</p>

```twig
{% include templatePath %}
```

<p style="text-align: justify;">
The way Jtwig resolves the given path to a specific resource is configurable and will be detailed later.
</p>

## `ignore missing` (optional)

<p style="text-align: justify;">
If Jtwig resource resolution is not able to find the given resource, <code>include</code> will, by default, throw an error. When the argument <code>ignore missing</code> is set, Jtwig will ignore missing resources and proceed with the rendering.
</p>

```twig
{% include templatePath ignore missing %}
```

## `with <expression>` (optional)

<p style="text-align: justify;">
The <code>with</code> argument adds the capability to provide model variables to the included template. The expression is expected to be evaluated as a map.
</p>

```twig
{% include templatePath with { key: 'value' } %}
```

## `only` (optional)

<p style="text-align: justify;">
The <code>only</code> argument tells the engine to isolate the included template from the parent context. That way variables currently defined in the context won't be visible in the included template.
</p>