# Resources

<p style="text-align: justify;">
Resources in Jtwig can be one of the following types:
</p>

- **`StreamResource`**, it's the most basic resource, it basically exposes a given stream as a Jtwig resource. Use this specific implementation with caution, be aware of `InputStream` statefull properties. Also this implementation has serious limitations when it comes to cache parsed Jtwig templates. Example:

```java
InputStream inputStream = new ...;
Resource resource = new StreamResource(inputStream);
```

- **`StringResource`**, a resource supporting Jtwig Template specifications using a Java String. This type of resource is useful to specify templates inlined with the code.

```java
Resource resource = new StringResource("Hello {{ variable }}!");
```

- **`FileResource`**, as the name can tell, uses a file as the reference to retrieve a Jtwig template.

```java
Resource resource = new FileResource(new File("<path to file>"));
```

- **`ClasspathResource`**, similar to a `FileResource` but useful when one want to render a template located in the application classpath. The classpath resource relies on the implementation of a `ClasspathResourceLoader`, which provides an interface for loading classpath resources and has a default implementation (`DefaultClasspathResourceLoader`).

```java
ClasspathResourceLoader classpathResourceLoader = new ...;
Resource resource = new ClasspathResource("<path>", classpathResourceLoader);
```


## Resource Resolver

<p style="text-align: justify;">
A Resource Resolver is the Jtwig component that resolves Resources, such resource is identified by the parent Resource and a path.
</p>

```java
Optional<Resource> resolve(Environment environment, Resource resource, String path);
```

<p style="text-align: justify;">
Note that it can only return a resource if it exists, otherwise it should return no result (<code>Optional::absent</code>).
</p>

**How it works?**
<p style="text-align: justify;">
While configuring Jtwig, has already shown in the Environment configuration, it's possible to specify multiple resource resolvers. Such list is then iterated in the same order they were added to the configuration, where the first resolver returning a non-empty result will be the one used.
</p>

**Default resolvers**

<p style="text-align: justify;">
When extending the default Jtwig configuration, it already comes with the following two resource resolvers:
</p>

1. ``FileResourceResolver``
2. ``ClasspathResourceResolver``


