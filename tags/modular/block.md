
# `block` construct

<p style="text-align: justify;">
A block construct plays two different roles depending on where it is placed. It can work as a placeholder with default content in parent templates or it can work as a content overrider in child templates.
</p>

<p style="text-align: justify;">
<b>Parent Template</b> is an extendable template, meaning that other templates can extend it. This templates do not contain the <code>extends</code> construct (as shown previously).
</p>

<p style="text-align: justify;">
<b>Child Templates</b> extend parent templates redefining its blocks. This templates contain the <code>extends</code> construct.
</p>

<p style="text-align: justify;">
A block has an associated identifier, used as the way to reference it within child templates.
</p>

```twig
{% block blockId %}
  ... content here ...
{% endblock %}
```

<p style="text-align: justify;">
From the previous example, the given block is identified with <code>blockId</code>, this mandatory identifier is also the only argument available for the block construct.
</p>

### `block` as content placeholder

<p style="text-align: justify;">
The <code>block</code> construct, as mentioned before, can be used as a content placeholder to define content that could be then replaced. A <code>block</code> is a content placeholder when used inside a parent template.
</p>

### `block` as content overrider

<p style="text-align: justify;">
The <code>block</code> construct, can also be used as a content overrider. This happens when the <code>block</code> is used underneath a child template.
</p>

### How does it work

<p style="text-align: justify;">
A block provides a way to change how a certain part of a template is rendered but it does not interfere in any way with the logic around it. Let’s take the following example to illustrate how a block works and more importantly, how it does not work:
</p>

```twig
{# block-base.twig #}
 
{% for post in posts %}
    {% block post %}
        <h1>{{ post.title }}</h1>
        <p>{{ post.body }}</p>
    {% endblock %}
{% endfor %}
```

<p style="text-align: justify;">
If you render this template, the result would be exactly the same with or without the block tag. The block inside the for loop is just a way to make it overridable by a child template:
</p>

```twig
{# block-child.twig #}
 
{% extends "block-base.twig" %}
 
{% block post %}
    <article>
        <header>{{ post.title }}</header>
        <section>{{ post.text }}</section>
    </article>
{% endblock %}
```

<p style="text-align: justify;">
Now, when rendering the child template, the loop is going to use the block defined in the child template instead of the one defined in the base one; the executed template is then equivalent to the following one:
</p>

```twig
{% for post in posts %}
    <article>
        <header>{{ post.title }}</header>
        <section>{{ post.text }}</section>
    </article>
{% endfor %}
```
