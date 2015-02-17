# Syntax

<p style="text-align: justify;">
Jtwig is a Twig port to Java, because of that Jtwig and Twig are very similar. However, Jtwig does not support all Twig features Twig, it contains functionality Twig does not offer and, finally, it also includes some small, yet important, differences at the syntax level. Within this section one will explain the Jtwig syntax in detail with special focus on the differences between Jtwig and Twig with the reasons behind such differences.
</p>

<p style="text-align: justify;">
Another aspect we will focus on in this book is comparison with other template engines in terms of functionality, specially the most widely used ones in the Java world.
</p>

<p style="text-align: justify;">
As a template language Jtwig allows one to have formatting logic around content. In order to do so, Jtwig uses the so called **Code Islands**.
</p>

## Code Islands

<p style="text-align: justify;">
As almost all template languages, Jtwig constructs can only be specified using code islands.
</p>

    {% ... Jtwig code here ... %}

<p style="text-align: justify;">
Jtwig code islands begin with `{%` and ends with `%}`, just as simple as that and exactly the same as Twig.
</p>

<p style="text-align: justify;">This differs from other template engines like [Thymeleaf](http://www.thymeleaf.org/) which constructs are defined with embedded code. Code islands allows to make a clear separation between template engine specific logic and the content, which is easier to read, locate and therefore to maintain.
</p>

### White space control

<p style="text-align: justify;">
Another syntatical construct 100% compatible with Twig is the white space control functionality. This allows one to remove white spaces before or after a code island. In order to accomplish that, append the symbol `-` to the beginning/ending of the Jtwig code island.</p>
<p style="text-align: justify;">Let's take an example:</p>

    {% ... jtwig code ... -%} text {%- ... jtwig code ... %}

<p style="text-align: justify;">
Such code will produce the inner `text` without white spaces.
</p>


## Identifier

<p style="text-align: justify;">
An identifier is a name in Jtwig, it can contain alphanumeric characters and also underscores, but cannot start with digits. This is exactly the same regular expression as Java identifiers.
</p>

    [A-Za-z_][A-Za-z_0-9$]*

<p style="text-align: justify;">
Of course such similarity happened on purpose, that way is possible to match specify any Java identifier in Jtwig, most importantly, when it comes to the selection operator (as explaned afterwards).
</p>

## Keywords

<p style="text-align: justify;">
One important thing to remember is that, there are reserver identifiers for Jtwig itself, known as keywords.
</p>

<table>
    <tr>
        <td>true</td>
        <td>false</td>
        <td>and</td>
        <td>or</td>
        <td>null</td>
        <td>set</td>
        <td>not</td>
        <td>is</td>
        <td>in</td>
    </tr>
    <tr>
        <td>include</td>
        <td>extends</td>
        <td>if</td>
        <td>elseif</td>
        <td>else</td>
        <td>endif</td>
        <td>block</td>
        <td>endblock</td>
    </tr>
</table>



## Operator Precedence

Descrever aqui os niveis de precedencia que tem.

