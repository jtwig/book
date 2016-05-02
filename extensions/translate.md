# Translate Extension

<p style="text-align: justify;">
The translate extension adds internationalization capabilities to Jtwig. It comes with two engines, the pluralization engine and the translation mechanism. Each of them with it's own tag and function.
</p>

### Translation

<p style="text-align: justify;">
The translation engine in Jtwig relies in two key pieces of information, the text to be translated and the desired language or, more specificaly, the locale.
</p>

### Pluralization

<p style="text-align: justify;">
Plural handling in Jtwig it's an easy to use and powerfull engine. Project <a href="https://github.com/jtwig/jtwig-pluralization">jtwig-pluralization</a> implements the underlying functionality.
</p>

**The counter (single)**

<p style="text-align: justify;">
This whole functionality derives from a key piece of information, the counter. Such counter is used to derive the plural form to be used, as so, this pluralization engine only supports one subject. For example, <code>1 apple and 2 oranges</code> contains two subjects, therefore, outside of this engine capabilities, such can be address, for example, by splitting the sentence into two.
</p>

<center>
<code>{0} No apples | {1} One apple | ]1, Inf[ Multiple apples</code>
</center>

<p style="text-align: justify;">
As per the previous example, the plural form contains three definitions (splitted by the <code>|</code> character). Definitions start with a range selector, which can either be a single value <code>{&lt;value&gt;}</code> or an interval of values, note that intervals can be inclusive or exclusive depending on the parentsis used. For example, <code>[1, 2]</code>, <code>]0, 3[</code>, <code>[1, 3[</code>, <code>]0, 2]</code> are all equivalent intervals.
</p>

<p style="text-align: justify;">
The pluralization engine also trims the selected value. It uses the <code>String:trim</code> method underneath.
</p>

**Function ``translateChoice``**

<p style="text-align: justify;">
This function is expecting two to four arguments. The two first arguments are mandatory, this is (1) the text to translate and (2) the counter, an integer value used, as mentioned already, to select the plural form.
</p>

<p style="text-align: justify;">
If three arguments are provided, the third argument can either be a string representing the locale to use, or, alternatively, a map of replacements to use. Both locale string representation and replacements concepts will be detailed further on.
</p>

<p style="text-align: justify;">
If four arguments are provided, the function will expect as third argument a map of replacements and then, as fourth argument, a string representing the locale to use.
</p>

```twig
{{ '{0} No apples | {1} One apple | ]1, Inf[ Multiple apples' 
    | translateChoice(numberOfApples, "pt") }}
```

<p style="text-align: justify;">
The previous example will look for a <code>pt</code> translation of the sentence <code>{0} No apples | {1} One apple | ]1, Inf[ Multiple apples</code>, then uses the pluralization engine to select, based on the counter (here defined as the variable <code>numberOfApples</code>), the plural form.
</p>