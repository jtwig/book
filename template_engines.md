# Template Engines

<p style="text-align: justify;">
To better understand the foundations of template engines it is best to start by clarifying what they are and what they do. What do projects benefit from using them and how do they affect projects, from the system design to its maintainability.
</p>

## What is a template engine?

<p style="text-align: justify;">
A template engine is a piece of software designed to combine a template with data model in order to produce a document. A template is an intermediate representation of the presentation. It specifies the rules that define on how the output will be generated.
</p>

<p style="text-align: justify;">
Let's take a look to one of the simplest template engines - the Java native <code>String.format</code>.
</p>


    String.format("Hello, I am %d years old", 30);

<p style="text-align: justify;">
Yes, String.format can be seen as a template engine, a really simple one. In the previous example, the content is the integer <code>30</code> which, when combined with the template Hello, <code>I am %d years old</code>, generates the output <code>Hello, I am 30 years old</code>.
</p>

## Why template engines? 

<p style="text-align: justify;">
In essence, a template engine allows one to split the content (data model), from its presentation, therefore allowing to develop the presentation and logic layer almost independently, where the only dependency is the data model. 
</p>

<p style="text-align: justify;">
Splitting this layers simplifies maintenance by increasing the application modularity and changeability. For example, during the initial stages of a project, both layers might have similar change rates, however, when the project enters the maintenance mode, the presentation layer tends to be more subject to change. Without a template engine, it would be required logic layer changes in order to modify the presentation.
</p>

<p style="text-align: justify;">
Another reason to adopt template engines is that, as tools written specifically for presentation logic development, they simplify their development by providing several useful functionalities.
</p>


## Why Jtwig?

<p style="text-align: justify;">
Jtwig appears from the desire of a better template engine in the Java world. After investigating all technologies available in the market, one decided to, instead of creating a brand new technology, port one good template engine to the Java world, mainly because one could only benefit from an already mature technology, heavily used and proven in the wild. Twig which is based on Django templates itself, was the choice. It was seen as the best alternative because of the following reasons:
</p>

- Code island based, making it easier to read when mixed with presentation content;
- Small learning curve, easy and common syntactic constructs, in fact, for Java developers, Jtwig has very similar building blocks;
- Simple yet powerful template inheritance mechanism;
- Great expressive power with the capability to create logical complex templates;


