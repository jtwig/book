# Chapter 1 : The Templating Science

## Introduction

<p style="text-align: justify;">
To better understand the fundations of template engines it is best to start by making clear what template engines are meant to do, what do projects benefit from using them and then how their design affects the project, from the system design to its maintainability.
</p>

<p style="text-align: justify;">
In essence, a template engine allows one to split the content from its presentation/formatting. Let's take a look to one of the simpliest template engines on earth - the Java native `String.format`.
</p>

    String.format("Hello, I am %d years old", 30);

<p style="text-align: justify;">
Yes, `String.format` can be seen as a template engine, a really simple one, but it does allow us to split the content from its presentation. Where the content is `30` which when combined with the **template** `Hello, I am %d years old` generates the output `Hello, I am 30 years old`.
</p>

#### Nomenclature

<p style="text-align: justify;">
In just few sentences we spoke about some simple, widely used yet not properly defined terms, *template engine* and *template*.
</p>

<p style="text-align: justify;">
**Template** Is an intermediate representation of the presentation. It specifies the rules that defines on how the output should be generated.
</p>

<p style="text-align: justify;">
**Template Engine** Is the component responsible of generating the output, it implements the rules specified in the template which together with the specified content assembles the final presentation.
</p>


### Why template engines?

<p style="text-align: justify;">
The main advantage of using a template engine is to split up the presentation layer from the logic layer. Of course, splitting a system into smaller components has its advantages and disadvantages, all of those already scrutinized a lot, but when it comes to splitting the presentation layer from the logic layer there are other aspects to take into account:
</p>

1. Different domains of knowledge
2. Different change rates

<p style="text-align: justify;">
When it comes to work on the presentation layer, for example, web technologies, there is a huge number of different languages and technologies that can be applied. Of course the same happens with the logic layer. Given the volume of technologies and required knowledge to handle them, splitting up this two decreases the need for full stack developers, which are more expensive. But also, allows expertise on each specific area to be fully used.
</p>

<p style="text-align: justify;">
Another benefit of splitting up this two layers is to simplify the maintenance due to the rate of change. In the initial stages of a project both layers have a similar change rate, however, when the project stabilizes, during the maintenance phase, the presentation layer would be more subject to change. By having this layers splitted no changes would be made to the logic layer for the purpose of modifying the presentation. Making the maintenance easier and therefore cheaper.
</p>

<p style="text-align: justify;">
"**Template engines eases the presentation layer development**"
</p>

<p style="text-align: justify;">
As tools written specifically for the development of the presentation logic, template engines represent an advantage in terms of effective cost for developing it providing various number of functionalities in that regard.
</p>

### How to choose which template engine to use?

<p style="text-align: justify;">
Essa é uma questão interessante (ver opiniões na web), que gera opiniões divergentes. Genericamente, partindo do seu fundamento principal, um bom sistema de template é (1) aquele que permite fazer uma boa separação entre camada de apresentação e camada de controlo. Neste contexto, para decidir qual sistema de template usar, é necessário analisar também qual o design pattern escolhido, do qual o sistema de template faz parte.
</p>

- Model View Controller (MVC)
- Model View ViewModel (MVVM)
- Model View Presenter (MVP)

..COMPLETAR..

<p style="text-align: justify;">
Também é importante analisar as caracteristicas do problema em questão. Trata-se de uma mera aplicação para apresentaçao de conteudos onde a apresentação não tem relevo? Ou será uma aplicação com construções de apresentação avançadas?
</p>

..COMPLETAR..

<p style="text-align: justify;">
Uma outra questão importante a ter em conta é a separação de tarefas, isto é, será a equipa responsavel pelo desenvolvimento uma equipa multidisciplinar capaz de lidar com logica de apresentacao e logica de controlo?
</p>

..COMPLETAR..

<p style="text-align: justify;">
Posteriormente, questões de ambito tecnico, como performance, security, etc., também ganham relevo em utilizacoes especificas.
</p>

<p style="text-align: justify;">
Tenha em atenção que no limite, um sistema de template será sempre mais lento que assemblar a resposta inline.
</p>

Em que agrupamento o Jtwig cabe..

Supports:

- Logical constructs
- Custom functions
- Custom syntax symbols
- Custom syntatic extensions



# Jtwig - Origins

<p style="text-align: justify;">
Jtwig origin is based on Twig for PHP, with the intent to be a Java port of this template engine. However, Java has it's own specifics has a web development tool. Based on that, Jtwig evolved to be more than a Twig port, becoming a flexible, integrated and powerful template engine, specially designed for web development.
</p>

## Why creating Jtwig?

<p style="text-align: justify;">
This question caught me a lot of times. Was not Java world already full of template engines? Why creating another one?
</p>

<p style="text-align: justify;">
I always wondered how can Java template engines syntax be so different from the Java syntax and why not a template engine designed for web development? Well, basically, I was unhappy with all used template engines, mainly because of:
</p>

- Their weird syntax
- Huge list of features/Lack of features
- Magic variables context (context switching)
- No easy out-of-the-box template inheritance

<p style="text-align: justify;">
In an ideal world, when it comes to Web Development with the use of MVC, the best template engine should be able to:
</p>

- Handle template inheritance fashionably
- Support the basic logic operations
- Extendable in every possible way
- Nice syntax

<p style="text-align: justify;">
Composition means more expressing power (more logic with less code).
</p>


## When should you use Jtwig?

<p style="text-align: justify;">
You should use Jtwig in complex scenarios, that is, when you need to handle complex logic in you view.
</p>

<p style="text-align: justify;">
Explicar o que significa complex logic neste contexto, se calhar, alterar essa descricao para algo mais positivo.
</p>


