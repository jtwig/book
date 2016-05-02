# Resources

<p style="text-align: justify;">
Resources in Jtwig are modeled as references. It uses the <code>ResourceReference</code> class to do so. A resource reference is a pair of type and path. For example:
</p>

- ``file:/tmp/file.twig`` represents a reference with type ``file`` and path ``/tmp/file.twig``
- ``classpath:template.twig`` refers to type ``classpath`` and path ``template.twig``.

**Reference Type**

<p style="text-align: justify;">
To represent the type one use a raw string, allowing for custom types to be introduced at configuration time. Each type must have an associated <code>ResourceLoader</code>, allowing one to, given a reference, perform different operations, like:
</p>

- **Load** reading the reference as an ``InputStream``.
- **Exists** check if the given reference exists.
- **URL** return the URL representation of the reference, if it exists.
- **Charset** return the charset of such reference, if possible.

**Types defined in Core**

<p style="text-align: justify;">
The Jtwig Core default configuration comes with three reference types, namely: 
</p>

- ``file``
- ``classpath``
- ``string``

**Absolute Type vs Relative Type**

<p style="text-align: justify;">
In Jtwig a reference type can either be relative or absolute, meaning that, relative path calculation is possible or not. For example, <code>file</code> and <code>classpath</code> types are relative types, while <code>string</code> is absolute.
</p>

**Relative Resource Resolver**

<p style="text-align: justify;">
For relative reference types only the concept of relative resource resolver exists so that, using a given reference as base path, calculate the path to another reference.
</p>

**The ``string`` reference**

<p style="text-align: justify;">
The <code>string</code> reference type is a special kind of reference where as path, one can provide, actually, a template definition. For example, the resource reference <code>string:{{ '{{ "hello world!" }}' }}</code> defines a resource with content <code>{{ '{{ "hello world!" }}' }}</code> which when rendered will produce <code>hello world!</code>.
</p>

**The ``any`` reference type**

<p style="text-align: justify;">
The resource resolution in Jtwig also allows one to refer to a given resource without specifying the type, as such, the defined type will be <code>any</code>, meaning a best effort approach will be used to load/resolve the given resource. For example to load the reference <code>/tmp/template.twig</code> (without the type) Jtwig will iterate over the list of <code>ResourceLoader</code> and the first one finding the resource will be used. For this is important the ordering defined during configuration. As default the ordering is as such:
</p>

- ``file`` with base directory as current working directory
- ``classpath`` using jtwig-core ``ClassLoader``

<p style="text-align: justify;">
Note that, the <code>string</code> type is ignored for the purpose of resource lookup.
</p>
