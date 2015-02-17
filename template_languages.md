# The Templating Science

<p style="text-align: justify;">
Para melhor perceber a problemática dos sistemas de templates é necessário olhar para o seu contributo numa análise profunda, que começa, como é natural, pelas suas bases.
</p>

<p style="text-align: justify;">
Na sua essencia um sistema de template resume-se a, partindo do conteudo, produzir texto apresentavel. Olhemos, por exemplo, para um dos mais basicos sistema de template existente.
</p>

    String.format("Hello, I am %d years old", 30);

<p style="text-align: justify;">
Sim, um simples `String.format` é um sistema de template. Como se pode observar, o conteudo é o valor `30` que quando combinado com o **template** - `"Hello, I am %d years old"`, isto é, a representação intermédia do sistema de template `String.format`, gera como resultado a frase `"Hello, I am 30 years old"`.
</p>

## Why template engines?

<p style="text-align: justify;">
Um dos grandes objetivos dos sistemas de templates passa por separar a camada de apresentação da camada lógica, permitindo dessa forma uma manutenção facilitada, aumentar drasticamente a testabilidade, bem como tornar os processos de desenvolvimento, tanto da componente lógica, como da componente de apresentação. Isto permite, como é obvio, aumentar a qualidade do codigo.
</p>

<p style="text-align: justify;">
Uma das grandes vantagens da utilização de templating num projeto é a vantagem inerente á separação do sistema em componentes mais pequenos, falamos nomeadamente da  testability. Isto é, ao criar um componente apenas responsavel pela geração de conteudo torna-se possivel validar o comportamento desse componente de forma isolada, tornando o teste muito mais simples quando comparado com o teste do resultado da composição de ambos.
</p>

<p style="text-align: justify;">
Um outro motivo para a utilizaçao de sistemas de template é a simplicidade, isto é, recorrendo a funcionalidades inatas dos sistemas de template torna-se mais simples especificar o formato da camada de apresentação.
</p>

## How to choose which template engine to use?

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


