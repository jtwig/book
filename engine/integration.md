# Integration

<p style="text-align: justify;">
Integrating Jtwig Core on your project is quite simple. It will mainly depend on the dependency management mechanism you use. You will need to make sure <code>jcenter</code> is part of your repository list. Such will allow you to get access to the <code>jtwig-core</code> dependency. To check the most recent version, go to <a target="_blank" href="https://bintray.com/jtwig/maven/jtwig-core/view">bintray</a>.
</p>

<p style="text-align: justify;">
For some integration examples check <a target="_blank" href="https://github.com/jtwig/jtwig-examples">jtwig-examples</a>.
</p>

### Gradle


```gradle
repositories {
    jcenter()
}
dependencies {
    compile 'org.jtwig:jtwig-core:5.X'
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
        <artifactId>jtwig-core</artifactId>
        <version>5.X</version>
    </dependency>
</dependencies>
```

### SBT

```sbt
libraryDependencies += "org.jtwig" % "jtwig-core" % "5.X"
```