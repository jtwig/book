# Jtwig Web

<p style="text-align: justify;">
Jtwig Web project extends Jtwig Core with and eases the integration with Java Servlet API (version 3.1). It also adds the function <code>path</code>, a new resource <code>WebResource</code> and resource resolver <code>WebResourceResolver</code>. 
</p>

### The ``path`` function

<p style="text-align: justify;">
The path function can be used to output the Servlet Context Path, for more information about this value, check the Servlet API documentation. It is expecting either none of one argument. If no argument is provided, as mentioned, it will only print the servlet context path, on the other hand, if the an argument is provided (expected to be a String), then it appends such value to the servlet context path.
</p>

```twig
{{ path('/index') }}
```

<p style="text-align: justify;">
Assuming the servlet context path is <code>/application</code>, then the previous example will output <code>/application/index</code>.
</p>

### The ``WebResource`` and ``WebResourceResolver``

<p style="text-align: justify;">
This combo of <code>WebResource</code> and <code>WebResourceResolver</code> allows Jtwig to support web (<code>WEB-INF/</code> rooted) resources. Users can then reference such resources from their app.  Note that, if a given path is prefixed with <code>web:</code>, it will be interpreted by this resource resolver, such can be used to disambiguate the source of those resources.
</p>

**Combining with the Servlet API**

<p style="text-align: justify;">
To integrate Jtwig Web with the Servlet API the <code>JtwigRenderer</code> concept was introduced.
</p>

```java
public static class HelloWorldServlet extends HttpServlet {
    private final JtwigRenderer renderer = JtwigRenderer.defaultRenderer();

    @Override
    protected void service(
        HttpServletRequest request, 
        HttpServletResponse response
        ) throws ServletException, IOException {
        request.setAttribute("variable", "Hello");

        renderer.dispatcherFor("/WEB-INF/templates/index.twig.html")
                .with("name", "Jtwig")
                .render(request, response);
    }
}
```

<p style="text-align: justify;">
The example above can be seen in <a href="https://github.com/jtwig/jtwig-examples/tree/master/gradle-jtwig-web-simple">jtwig-examples</a>. It will print <code>Hello World!</code>, as the <code>/WEB-INF/templates/index.twig.html</code> template is defined as <code>{{ '{{ variable }} {{ name }}!' }}</code>. As one can see in the previous example, <code>JtwigRenderer</code> exposes all request variable as part of the <code>JtwigModel</code> passed to the render stage.
</p>

<p style="text-align: justify;">
Note that, this <code>JtwigRenderer</code> also exposes an API call to specify the Jtwig template inline, as shown in the example below. Such example will produce the same output as the example above.
</p>

```java
public class HelloWorldServlet extends HttpServlet {
    private final JtwigRenderer renderer = JtwigRenderer.defaultRenderer();

    @Override
    protected void service(
            HttpServletRequest request,
            HttpServletResponse response
    ) throws ServletException, IOException {
        request.setAttribute("variable", "Hello");

        renderer.inlineDispatcherFor("{{ variable }} {{ name }}!")
                .with("name", "Jtwig")
                .render(request, response);
    }
}
```


**The ``app`` variable**

<p style="text-align: justify;">
<code>JtwigRenderer</code> injects into the <code>JtwigModel</code> the <code>app</code> variable which exposes information extracted from the <code>HttpServletRequest</code> provided.
</p>

```java
public class Application {
    private HttpRequest request;
}
```

```java
public class HttpRequest {
    private Map<String, Object> parameter;
    private Map<String, Object> query;
    private Map<String, Object> session;
    private Map<String, Object> cookies;
}
```

<p style="text-align: justify;">
This allows one to access:
</p>

* GET query parameters (using ``app.request.query.parameterName``)
* POST parameters (using ``app.request.parameter.parameterName``)
* Session parameters (using ``app.request.session.parameterName``)
* Cookie parameters (using ``app.request.cookies.parameterName``)

## Integration

<p style="text-align: justify;">
Integration of Jtwig Web in your project will depend on the dependency management mechanism being used. Also, you will need to make sure <code>jcenter</code> is part of your repository list. To check the most recent version, go to <a target="_blank" href="https://bintray.com/jtwig/maven/jtwig-web/view">bintray</a>.
</p>


### Gradle


```gradle
repositories {
    jcenter()
}
dependencies {
    compile 'org.jtwig:jtwig-web:1.X'
}
```


### Maven

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
        <artifactId>jtwig-web</artifactId>
        <version>1.X</version>
    </dependency>
</dependencies>
```