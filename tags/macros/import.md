# `import` construct

<p style="text-align: justify;">
The <code>import</code> tag is the way to reuse defined macros, it affects the model, adding a variable containing all macros defined in a specific Jtwig template resource.
</p>

```twig
{% import resourcePath as macros %}
```

<p style="text-align: justify;">
As shown in the previous example, all macro definitions inside <code>resourcePath</code> will be amalgamated in the <code>macros</code> variable, so called the <b>alias</b>.
</p>

***

### How to use?

<p style="text-align: justify;">
To call a macro, one just need to use the alias together with the desired macro name and its arguments.
</p>

```twig
{{ macros.macroName(argument1, argument2) }}
```

<p style="text-align: justify;">
Let's then have a look to the example below.
</p>

**File: `forms.twig`**
```twig
{% macro text (name, defaultValue) %}
<input name="{{ name }}" type="text" value="{{ defaultValue }}" />
{% endmacro %}
```

**File: `template.twig`**
```twig
{% import 'forms.twig' as forms %}
{{ macros.text('username') }}
```

<p style="text-align: justify;">
As one can see from the previous example, the template <code>template.twig</code> imports all macro definitions from <code>forms.twig</code> into the alias <code>forms</code>. It then renders the <code>text</code> macro providing only one argument <code>'username'</code>.
</p>

### Argument resolution

<p style="text-align: justify;">
As mentioned before, macro arguments are all optional. In the previous example, the macro defined two arguments <code>name</code> and <code>defaultValue</code>, however the call only provided one argument. The way arguments are feeded into the macro is by the order specified. In the previous example, the provided argument <code>'username'</code> will then be represented by the identifier <code>name</code> in macro specification.
</p>