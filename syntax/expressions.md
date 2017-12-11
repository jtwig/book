## Expressions

<p style="text-align: justify;">
Expressions are the logic building blocks, they allow you to express a value. From the basic constants to binary and ternary operations, expressions give developers the power to specify a value.
</p>

### Literals

<p style="text-align: justify;">
The most basic expressions, check the table below.
</p>

| Name    | Regular Expression  |
|---------|---------------------|
| Float | `-?[0-9]+'.'[0-9]+` |
| Integer | `-?[0-9]+` |
| Null Reference | `null` |
| Boolean | `true` or `false` |
| String | `"[^"]*"` or `'[^']*'` |
| Character | `'[a-zA-Z]'` |

### Identifier

<p style="text-align: justify;">
An identifier is a name in Jtwig. It can contain alphanumeric characters and also underscores, but cannot start with digits. This is exactly the same regular expression as Java identifiers.
</p>

    [a-zA-Z_$][a-zA-Z0-9_$]*

<p style="text-align: justify;">
Of course such similarity happens on purpose, making it possible to specify any Java identifier in Jtwig templates. Such capability enables Jtwig to be fully compatible with Java identifiers, an important feature, specially, when it comes to the selection operator (as explained later on). This is one of the fundamental differences between Twig and Jtwig. Their regular expressions for identifiers are different and they match exactly the expression defined by their mother language. However different, they are quite similar. As per PHP official documentation PHP Manual, identifiers are defined according to the following regular expression:
</p>

    [a-zA-Z_\x7f-\xff][a-zA-Z0-9_\x7f-\xff]*

<p style="text-align: justify;">
PHP definition is very similar to Java’s one, apart from the <code>$</code> character, however it also includes bytes from 127 to 225 (\x7f-\xff). Depending on the encoding, these extra bytes might be latin characters or even punctuation.
</p>

<p style="text-align: justify;">
This allows one to create Jtwig and Twig compatible templates, nevertheless, it is important to be aware of such differences in order to accurately measure compatibility.
</p>


### List

<p style="text-align: justify;">
There are two ways to specify a list in Jtwig. It can be either by enumeration or by comprehension. To specify a list by enumeration, one basically need to provide every single element of the list, as shown below.
</p>

    [1, 2, 3]

<p style="text-align: justify;">    
To specify a list by comprehension, however, one just need to specify both the beginning and the ending elements of the list, Jtwig engine, will then expand the definition. Currently, it only supports Integers or Characters.
</p>

    1..3

<p style="text-align: justify;">    
Both lists, exemplified above, produce the same output.
</p>

### Maps

<p style="text-align: justify;">
It is also possible to represent collections of key and value pairs in Jtwig, so called maps, where keys can either be Identifiers or Strings and values can take form of any kind of expression.
</p>

    { key1: 'value1', 'key 2': 'value2' }

<p style="text-align: justify;">
Keep in mind that identifiers used to represent the key elements are not used as variable placeholders, instead, they are converted to their String representation. For example, the identifier <code>key1</code> shown above will be converted to the String value <code>"key1"</code>.
</p>

### List or Map Value Access

<p style="text-align: justify;">
Whenever one need to access either a list element or map value, Jtwig, like Twig, comes with the value access expression. With such expression one can access the value given the key. Note that, for lists, the key is the position of the element in the list starting at zero.
</p>

    list[1]
    map[“hello”]


### Keywords

<p style="text-align: justify;">
Jtwig has some reserved identifiers, such identifiers are the building blocks of more complex Jtwig constructs. Below there is the list of the native reserved identifiers. 
</p>

<p style="text-align: center;">
    <code>include</code> <code>set</code> <code>block</code> <code>endblock</code> <code>if</code> <code>endif</code> <code>elseif</code> <code>else</code> <code>for</code> <code>endfor</code> <code>import</code> <code>macro</code> <code>endmacro</code> <code>extends</code> <code>embed</code> <code>endembed</code> <code>true</code> <code>false</code> <code>in</code> <code>as</code> <code>autoescape</code> <code>endautoescape</code> <code>do</code> <code>flush</code> <code>verbatim</code> <code>endverbatim</code> <code>spaceless</code> <code>endspaceless</code> <code>filter</code> <code>endfilter</code> <code>null</code> <code>is</code> <code>not</code> <code>with</code>
</p>

<p style="text-align: justify;">
Note that Jtwig is extensible and the list of keywords might be affected by such extensions.
</p>

### Unary Operators

<p style="text-align: justify;">
Unary operators by definition only need one argument, Jtwig comes with only two built in unary operators, they are <code>not</code> and <code>-</code>.
</p>

| Operator | Symbol | P<span style="text-transform: superscript;">*</span> | Description | Example |
|----------|--------|---|-------------|---------|
| Negative | `-` | 5 | Switches the signal. | `-(-1)` outputs `1`|
| Not | `not` | 10 | Negates the input. | `not false` outputs `true` </br> `not true` outputs `false` |

<span style="text-transform: superscript;">*</span> Precedence order, the lower the precedence, the higher the priority. 

### Binary Operators

<p style="text-align: justify;">
Jtwig comes with several built in binary operators. Below, one will describe the entire list of built in binary operators.
</p>

<table>
    <thead>
        <tr>
            <th style="width: 10%;">Operator</th>
            <th>Symbol</th>
            <th>P</th>
            <th style="width: 30%;">Description</th>
            <th>Example</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>Selection</td>
            <td style="text-align: center;"><code>.</code></td>
            <td style="text-align: center;">1</td>
            <td>Access inner properties of objects.</td>
            <td><code>[1, 2].size</code> outputs <code>2</code>
            </td>
        </tr>
        <tr>
            <td>Multiply</td>
            <td style="text-align: center;"><code>*</code>
            </td>
            <td style="text-align: center;">5</td>
            <td>Multiplies two values.</td>
            <td><code>5.0 * 2.5</code> outputs <code>12.5</code>
            </td>
        </tr>
        <tr>
            <td>Integer Multiply</td>
            <td style="text-align: center;"><code>**</code>
            </td>
            <td style="text-align: center;">5</td>
            <td>Multiplies the integer part of two values.</td>
            <td><code>5.0 ** 2.5</code> outputs <code>10</code>
            </td>
        </tr>
        <tr>
            <td>Divide</td>
            <td style="text-align: center;"><code>/</code>
            </td>
            <td style="text-align: center;">5</td>
            <td>Divides two values.</td>
            <td><code>5.0 / 2.5</code> outputs <code>2</code>
            </td>
        </tr>
        <tr>
            <td>Integer Divide</td>
            <td style="text-align: center;"><code>//</code>
            </td>
            <td style="text-align: center;">5</td>
            <td>Divides the integer part of two values.</td>
            <td><code>5.0 // 2.5</code> outputs <code>2.5</code>
            </td>
        </tr>
        <tr>
            <td>Remainder</td>
            <td style="text-align: center;"><code>%</code>
            </td>
            <td style="text-align: center;">5</td>
            <td>Gets the integer division remainder.</td>
            <td><code>5 % 2</code> outputs <code>1</code>
            </td>
        </tr>
        <tr>
            <td>Sum</td>
            <td style="text-align: center;"><code>+</code>
            </td>
            <td style="text-align: center;">10</td>
            <td>Sums two values.</td>
            <td><code>5 + 2</code> outputs <code>7</code>
            </td>
        </tr>
        <tr>
            <td>Subtract</td>
            <td style="text-align: center;"><code>-</code>
            </td>
            <td style="text-align: center;">10</td>
            <td>Subtracts two values.</td>
            <td><code>5 - 2</code> outputs <code>3</code>
            </td>
        </tr>
        <tr>
            <td>Concat</td>
            <td style="text-align: center;"><code>~</code>
            </td>
            <td style="text-align: center;">10</td>
            <td>Concatenates two strings.</td>
            <td><code>"5" ~ "2"</code> outputs <code>"52"</code>
            </td>
        </tr>
        <tr>
            <td>Less</td>
            <td style="text-align: center;"><code>&lt;</code>
            </td>
            <td style="text-align: center;">15</td>
            <td>Compares two values, checking whether the first is lower than the second.</td>
            <td><code>1 &lt; 2</code> outputs <code>true</code>
                <br> <code>1 &lt; 1</code> outputs <code>false</code>
            </td>
        </tr>
        <tr>
            <td>Less or equal</td>
            <td style="text-align: center;"><code>&lt;=</code>
            </td>
            <td style="text-align: center;">15</td>
            <td>Compares two values, checking whether the first is lower or equal than the second.</td>
            <td><code>2 &lt;= 2</code> outputs <code>true</code>
                <br> <code>2 &lt; 1</code> outputs <code>false</code>
            </td>
        </tr>
        <tr>
            <td>Greater</td>
            <td style="text-align: center;"><code>&gt;</code>
            </td>
            <td style="text-align: center;">15</td>
            <td>Compares two values, checking whether the first is higher than the second.</td>
            <td><code>2 &gt; 1</code> outputs <code>true</code>
                <br> <code>2 &gt; 2</code> outputs <code>false</code>
            </td>
        </tr>
        <tr>
            <td>Greater or equal</td>
            <td style="text-align: center;"><code>&gt;=</code>
            </td>
            <td style="text-align: center;">15</td>
            <td>Compares two values, checking whether the first is higher or equal than the second.</td>
            <td><code>2 &gt;= 2</code> outputs <code>true</code>
                <br> <code>2 &gt;= 3</code> outputs <code>false</code>
            </td>
        </tr>
        <tr>
            <td>Contains</td>
            <td style="text-align: center;"><code>in</code>
            </td>
            <td style="text-align: center;">15</td>
            <td>Checks whether the second value contains the first one.</td>
            <td><code>5 in [2]</code> outputs <code>false</code>
            </td>
        </tr>
        <tr>
            <td>Equivalent</td>
            <td style="text-align: center;"><code>==</code>
            </td>
            <td style="text-align: center;">20</td>
            <td>Compares two values, checking whether they are equal or not.</td>
            <td><code>true == false</code> outputs <code>false</code>
                <br> <code>false == false</code> outputs <code>true</code>
            </td>
        </tr>
        <tr>
            <td>Different</td>
            <td style="text-align: center;"><code>!=</code>
            </td>
            <td style="text-align: center;">20</td>
            <td>Compares two values, checking whether they are different or not.</td>
            <td><code>true != false</code> outputs <code>true</code>
                <br> <code>false != false</code> outputs <code>false</code>
            </td>
        </tr>
        <tr>
            <td>And</td>
            <td style="text-align: center;"><code>and</code>
            </td>
            <td style="text-align: center;">25</td>
            <td>Conjunction boolean operator.</td>
            <td><code>true and false</code> outputs <code>false</code>
                <br> <code>true and true</code> outputs <code>true</code>
            </td>
        </tr>
        <tr>
            <td>Or</td>
            <td style="text-align: center;"><code>or</code>
            </td>
            <td style="text-align: center;">25</td>
            <td>Disjunction boolean operator.</td>
            <td><code>true or false</code> outputs <code>true</code>
                <br> <code>false or false</code> outputs <code>false</code>
            </td>
        </tr>
        <tr>
            <td>Compose</td>
            <td style="text-align: center;"><code>|</code>
            </td>
            <td style="text-align: center;">30</td>
            <td>Uses the first argument as parameter for the second argument. Note that, composition forces the second argument to be a function.</td>
            <td><code>-5 | abs</code> outputs <code>5</code>
            </td>
        </tr>
    </tbody>
</table>


### Ternary Operator

<p style="text-align: justify;">
Jtwig only contains one ternary operator. It allows to fork the behaviour based on a boolean expression, as exemplified below.
</p>

    expr ? 1 : 2

<p style="text-align: justify;">
Such expression will output <code>1</code> if the variable <code>expr</code> is true, or <code>2</code> if the variable is false.
</p>

### Test

<p style="text-align: justify;">
Test expressions are a complex predicate construct, they return a boolean value as result. Jtwig comes with some built in tests.
</p>

| Name | Description | Example |
|------|-------------|---------|
| Null | Checks whether a value is null or not. | `1 is null` outputs `false` |
| Divisible | Checks if a value is divisible by another. | `2 is divisible by 1` outputs `true` |
| Same As | Checks whether two objects are, actually, the same. Note that this uses the Java `==` operator between the two given operands. | `1 is same as 2` outputs `false` |
| Function based | This construct is based on the available list of functions defined in Jtwig. It even allows one to use user defined functions in a test expression. | `4 is defined` outputs `true`. Note that `defined` is a function from the built in list of functions. |
| Is Not | All test constructs listed before can be negated with the `is not` constructor. | `4 is not defined` outputs `false` </br> `1 is not null` outputs `true` |


### Selection Operator

<p style="text-align: justify;">
The selection operator uses multiple strategies to extract properties or execute a method from a given identifier. An identifier in Jtwig can either specify a native Java object or a macro import. In this section one will only detail how the extracting of Java native object properties works. Lets start with two simple examples:
</p>

    var.p1
    var.method1(2)

<p style="text-align: justify;">
The first expression above specifies a selection operation to extract property <code>p1</code> from <code>var</code> object. The second expression however is providing an argument, such feature allows Jtwig to execute Java methods. By default, there are several different strategies used to extract values from a Java object. All strategies are applied until one of them gets a value. It tries each strategy in the following order:
</p>

**Method with the same name**

<p style="text-align: justify;">
In this strategy the given object meta information is searched, using reflection, for methods with the exact same name (case sensitive comparison) as the property name provided. Using the previous examples, it would search for a method with name <code>p1</code> without arguments given the first expression, where for the second expression it will search for a method, again, with the same exact name and the same number of arguments.
</p>

**Method prefixed with `get`, `is` or `has`**

<p style="text-align: justify;">
Similar to the previous strategy but instead of searching for an exact match, it looks for methods with the <code>get</code>, <code>is</code> or <code>has</code> prefixes. As per previous first example, it would try to find in the following order <code>getP1</code>, <code>isP1</code> or <code>hasP1</code>. As exemplified, the first letter of the given property name is capitalized. Once again such comparisons are case sensitive. This strategy also works with arguments, exactly the same the previous strategy works.
</p>

**Field with the same name**

<p style="text-align: justify;">
This strategy searches for fields with the exact same name as provided, the name comparison is case sensitive. 
</p>

**Map key with the same name**

<p style="text-align: justify;">
Is a strategy that only works against map objects and basically represents another way of accessing values in a map using the key as the property name.
</p>
