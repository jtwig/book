# Jtwig Spring Boot

<p style="text-align: justify;">
The <code>jtwig-spring-boot-starter</code> project allows one to easily integrate Jtwig with <a href="http://projects.spring.io/spring-boot/">Spring Boot</a>. Just by adding the dependency to your project, spring-boot will then load <code>JtwigViewResolver</code>.
</p>

### Integrate

<p style="text-align: justify;">
Check the most recent version, go to <a target="_blank" href="https://bintray.com/jtwig/maven/jtwig-spring-boot-starter/view">bintray</a>.
</p>

**Gradle**

```gradle
repositories {
    jcenter()
}
dependencies {
    compile 'org.jtwig:jtwig-spring-boot-starter:5.X'
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
        <artifactId>jtwig-spring-boot-starter</artifactId>
        <version>5.X</version>
    </dependency>
</dependencies>
```


### Default Configuration

<p style="text-align: justify;">
If you include jtwig-spring-boot-starter in your project, by default it will set the view resolver with prefix <code>classpath:/templates/</code>, suffix will be set as <code>.twig</code> and the Jtwig default configuration will be used. Note that, jtwig-spring-boot-starter uses jtwig-web which extends the default Jtwig Core configuration, as already mentioned.
</p>

### Costumize Configuration

<p style="text-align: justify;">
It is still possible to customize <code>JtwigViewResolver</code> to define prefix, suffix and also Jtwig Environment. For that <code>JtwigViewResolverConfigurer</code> interface can be extended by <code>@Configuration</code> annotated class. Note that, such class needs to be injected by spring-boot to the application context.
</p>

```java
@Configuration
public class JtwigConfig implements JtwigViewResolverConfigurer {
    @Override
    public void configure(JtwigViewResolver viewResolver) {
        viewResolver.setRenderer(new JtwigRenderer(EnvironmentConfigurationBuilder
                .configuration()
                .extensions().add(new MyExtension()).and()
                .build()));
    }

    private static class MyExtension implements Extension {
        @Override
        public void configure(EnvironmentConfigurationBuilder configurationBuilder) {
            System.out.println("Hi");
        }
    }
}
```


<p style="text-align: justify;">
The previous example sets the <code>JtwigViewResolver</code> renderer with an extended version of the <code>EnvironmentConfiguration</code> including a dummy <code>Extension</code>. This working example can be found in <a href="https://github.com/jtwig/jtwig-examples/tree/master/gradle-jtwig-spring-boot-simple">jtwig-examples</a>.
</p>