# Translate Extension

<p style="text-align: justify;">
The translate extension adds internationalization capabilities to Jtwig. It heavily relies on the concept of <code>MessageSource</code>, which will be detailed futher on. This extension is highly configurable and can be optimized for each specific use case.
</p>

### Translation

<p style="text-align: justify;">
The translation engine in Jtwig relies in two distinct concepts:
</p>

* Message Source
* Message Decoration

**Message Source**

<p style="text-align: justify;">
Message source mechanism acts as a storage of translations, it allows one to get translations of text to another language, more specifically, to a Locale (check the official Java documentation <code>java.util.Locale</code>). In Jtwig, if such message source engine is unable to find a requested translation, then it returns the given text.
</p>

<blockquote>
    <strong>Key</strong> and <strong>Free Text</strong>

    <p style="text-align: justify;">
    There are two typical approaches used as input for translations. It is either a <strong>Key</strong> or <strong>Free Text</strong>. The difference between this two approaches is that keys aren't readable, while the provided free text can be. Because keys are not shown to the end-user (at least they shouldn't), they can incorporate contextual information, like the purpose of the text, for example, <code>registration.title</code> or <code>registration.subtitle</code>. Free text approaches tend to define the wording directly, for example, <code>Register</code> or <code>Please, fill the form below and submit</code>. Jtwig allows for both approaches, where, for example, properties files can be used with the <strong>Key</strong> approach and Jtwig XLIFF can be used for the <strong>Free Text</strong> one.
    </p>
    <p style="text-align: justify;">
    We believe translations should be context independent, that is, locating a given text or identifying the purpose of a given text should not be the purpose of a translation mechanism. However, given the size of some platforms, decouple this two concepts can cause more harm than good.
    </p>
</blockquote>

**Message Decoration**

<p style="text-align: justify;">
Message decoration is the engine which allows one to modify the output of the message source. Jtwig translate extension makes use of a replacement strategy as decorator, allowing users to specify a map of replacements to modify the output, such will be detailed further on.
</p>


### Configuration


```java
TranslateConfiguration configuration = TranslateConfigurationBuilder
                .translateConfiguration()
                    .withCurrentLocaleSupplier(currentLocaleSupplier)
                    .withStringLocaleResolver(localeResolver)
                    .withMessageSourceFactory(messageSourceFactory)
                .build();
```


<p style="text-align: justify;">
As mentioned this extension is highly configurable, it allows, as seen in the example above, to specify a <code>LocaleResolver</code>, a locale supplier and a <code>MessageSourceFactory</code>.
</p>

**Locale Supplier**

<p style="text-align: justify;">
A locale supplier gives Jtwig the capability to retrieve a locale from the context when no locale is specified. By default Jtwig returns a static supplier which returns <code>Locale.ENGLISH</code> as result.
</p>

**LocaleResolver**

<p style="text-align: justify;">
The locale resolver is used to convert a raw String to a <code>java.util.Locale</code>, by default Jtwig will use the <code>Locale::forLanguageTag</code> method provided by the Java API.
</p>

**MessageSourceFactory**

<p style="text-align: justify;">
The message source factory gets called when Jtwig is initializing the environment, it can be used to preload resources and provide and instance of the <code>MessageSource</code> interface.
</p>

```java
public interface MessageSourceFactory {
    MessageSource create (Environment environment);
}
```

<p style="text-align: justify;">
Jtwig provides several implementations of such factory. A singleton factory <code>SingletonMessageSourceFactory</code>, which only returns the provided <code>MessageSource</code> instance. A cached factory <code>CachedMessageSourceFactory</code> allowing to, given a specific cache implementation, put it in front of the generated <code>MessageSource</code>. Shipped within this extension it's also the <code>PropertiesMessageSourceFactoryBuilder</code> which give the developer a nice API to create a <code>MessageSourceFactory</code> to load messages from properties files.
</p>

<blockquote>
    <strong>Jtwig XLIFF</strong>
    <p style="text-align: justify;">
    Jtwig XLIFF was developed as a way to support XLIFF defined translation files. It comes with a <code>XliffMessageSourceFactoryBuilder</code> quite similar to the properties message source factory.
    </p>
</blockquote>

**Function ``translate``**

<p style="text-align: justify;">
This function has two other alias, they are <code>trans</code> and <code>message</code>. It expects one argument at least, with the possibility of receiving two extra, optional, arguments. The first mandatory argument is the text to be translated. 
</p>

```twig
{{ translate('Hello World') }}
```

<p style="text-align: justify;">
If two arguments are provided it can either be a Locale, represented as a string or a map of replacements.
</p>

```twig
{{ translate('Hello World', 'pt') }}
```

```twig
{{ translate('Hello %name%', {'%name%': 'Jtwig'}) }}
```


<p style="text-align: justify;">
If a map is provided Jtwig will use it as replacements applying to the message returned by the message source. Otherwise, if a string is provided, Jtwig will ask the message source mechanism for a given message with the locale provided.
</p>

```twig
{{ translate('Hello World', {'%name%': 'Jtwig'}, 'pt') }}
```

<p style="text-align: justify;">
If three arguments are provided, then the map is expected as second argument and a string, representing a locale, the third.
</p>

**The ``trans`` tag**

<p style="text-align: justify;">
The <code>trans</code> tag has the same capabilities as the <code>translate</code> function allowing to specify the text to translate as body.
</p>

```twig
{% trans %}Hello world{% endtrans %}
```

```twig
{% trans into 'pt' %}Hello world{% endtrans %}
```

```twig
{% trans with {'%name%': 'Jtwig'} into 'pt' %}Hello %name%{% endtrans %}
```

```twig
{% trans with {'%name%': 'Jtwig'} %}Hello %name%{% endtrans %}
```

<p style="text-align: justify;">
Note that, the text is trimmed before querying the message source for the translation.
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
This function allows for the same capabilities as the <code>translate</code> plus choosing the plural form to use after processing the translation.
</p>

```twig
{{ '{0} No apples | {1} One apple | ]1, Inf[ Multiple apples' 
    | translateChoice(numberOfApples, "pt") }}
```

<p style="text-align: justify;">
The previous example will look for a <code>pt</code> translation of the sentence <code>{0} No apples | {1} One apple | ]1, Inf[ Multiple apples</code> and, only after retrieving the translation, uses the pluralization engine to select, based on the counter (here defined as the variable <code>numberOfApples</code>), the plural form.
</p>


### Integration

<p style="text-align: justify;">
Integrating Jtwig Translation Extension on your project is quite simple with the help of dependency managers. To check the most recent version, go to <a target="_blank" href="https://bintray.com/jtwig/maven/jtwig-translation-extension/view">bintray</a>.
</p>

**Gradle**


```gradle
repositories {
    jcenter()
}
dependencies {
    compile 'org.jtwig:jtwig-translation-extension:1.X'
}
```


**Maven**

```xml
<repositories>
    <repository>
        <id>bintray</id>
        <url>https://jcenter.bintray.com/</url>
    </repository>
</repositories>

<dependencies>
    <dependency>
        <groupId>org.jtwig</groupId>
        <artifactId>jtwig-translation-extension</artifactId>
        <version>1.X</version>
    </dependency>
</dependencies>
```

**Examples**

<p style="text-align: justify;">
Check the <a href="https://github.com/jtwig/jtwig-examples">jtwig-examples</a> project on github for examples using this translation engine.
</p>