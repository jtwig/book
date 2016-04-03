## Code Islands

<p style="text-align: justify;">
As a template language, Jtwig allows one to have formatting logic around content. In order to do so, Jtwig uses the so called Code Islands. This is similar to many template languages and identical to Twig’s syntax.
</p>

```twig
{% ... Jtwig code here ... %}
```

<p style="text-align: justify;">
Jtwig code islands begin with <code>{{ '{%' }}</code> and ends with <code>{{ '%}' }}</code>, just as simple as that.
</p>

## White space control

<p style="text-align: justify;">
Tied up with the code island syntax is another syntactical enabled feature, 100% compatible with Twig, the white space control functionality. This allows one to remove white spaces before or after a code island. In order to accomplish that, append/prepend the symbol <code>-</code> to the beginning/ending of the Jtwig code island. Let's take for example:
</p>

```twig
{% ... jtwig code ... -%} text {%- ... jtwig code ... %}
```

<p style="text-align: justify;">
Such code will produce <code>text</code> without white spaces. 
</p>

## Comments

<p style="text-align: justify;">
In Jtwig there are only multiline comments.
</p>

```twig
{# This is the content of the comment. 
    And it can be a multi-line content.  #}
```

<p style="text-align: justify;">
Note that comments also support the white space control feature, using the same approach as per code islands.
</p>

```twig
{#- Comment... -#}
```

## Output

<p style="text-align: justify;">
In Jtwig there is only one way to write the value of an expression (the definition of expression will be detailed afterwards) to the output. That is accomplished with the print operation as shown below.
</p>

```twig
{{ expression... }}
```

<p style="text-align: justify;">
Output constructs also support white space control feature in the same way as code islands.
</p>

```twig
{{- expression... -}}
```

