# Jtwig Spring

## Project ``jtwig-spring``

<p style="text-align: justify;">
The <code>jtwig-spring</code> project includes implementations of Spring <code>View</code> and <code>ViewResolver</code>, allowing one to integrate Jtwig with Spring MVC.
</p>

```java
@Configuration
@EnableWebMvc
public class WebConfig {
    @Bean
    public ViewResolver viewResolver () {
        JtwigViewResolver viewResolver = new JtwigViewResolver();
        viewResolver.setPrefix("web:/WEB-INF/templates/");
        viewResolver.setSuffix(".twig.html");
        return viewResolver;
    }
}
```

<p style="text-align: justify;">
The example above defines the <code>ViewResolver</code> bean used by Spring MVC to render a given view. The example shown here can be found in <a href="https://github.com/jtwig/jtwig-examples/tree/master/gradle-jtwig-spring-simple">jtwig-examples</a>.
</p>

## Integrating

<p style="text-align: justify;">
Integrating Jtwig Spring on your project is quite simple with the help of dependency managers. To check the most recent version, go to <a target="_blank" href="https://bintray.com/jtwig/maven/jtwig-spring/view">bintray</a>.
</p>

### Gradle


```gradle
repositories {
    jcenter()
}
dependencies {
    compile 'org.jtwig:jtwig-spring:5.X'
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
        <artifactId>jtwig-spring</artifactId>
        <version>5.X</version>
    </dependency>
</dependencies>
```
