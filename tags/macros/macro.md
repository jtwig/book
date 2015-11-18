# `macro` construct

<p style="text-align: justify;">
The <code>macro</code> tag gives users a way to specify pieces of reusable templates by also allowing it to received arguments.
</p>

```twig
{% macro macroName (firstArgument, secondArgument, ...) %}
  ... reusable template content ....
{% endmacro %}
```


### Macro Name

<p style="text-align: justify;">
The macro name is an identifier used to reference the macro. It must be unique inside a Jtwig template file. There is no validation on macro name duplication, reusing a macro name within the same template file will only override the previous definition.
</p>

### Macro Arguments

<p style="text-align: justify;">
Macro arguments is a list of identifiers representing input variables which can then be used inside the macro body definition. All arguments are optional, is up to the caller to provide such arguments or not.
</p>