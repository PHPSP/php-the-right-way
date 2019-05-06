---
layout: page
title: Design Patterns
---

# Design Patterns (Padrões de Projeto)

Existem diversas formas de estruturar o código e o projeto da sua aplicação web e você pode gastar muito ou pouco
esforço pensando na sua arquitetura. Mas geralmente é uma boa ideia seguir à padrões comuns, pois isso irá fazer com que
 seu código seja mais fácil de manter e de ser entendido por outros desenvolvedores.

* [Padrões de Arquitetura na Wikipedia](https://en.wikipedia.org/wiki/Architectural_pattern)
* [Padrões de Design de Software na Wikipedia](https://en.wikipedia.org/wiki/Software_design_pattern)
* [Coleção de exemplos de implementação](https://github.com/domnikl/DesignPatternsPHP)

## Factory (Fábrica)

Um dos padrões de design mais utilizados é o padrão "Factory" (Fábrica). Através dele uma classe simplesmente
cria o objeto que você gostaria de usar. Considere o seguinte exemplo desse padrão de design:

{% highlight php %}
<?php
class Automobile
{
    private $vehicle_make;
    private $vehicle_model;

    public function __construct($make, $model)
    {
        $this->vehicle_make = $make;
        $this->vehicle_model = $model;
    }

    public function get_make_and_model()
    {
        return $this->vehicle_make . ' ' . $this->vehicle_model;
    }
}

class AutomobileFactory
{
    public static function create($make, $model)
    {
        return new Automobile($make, $model);
    }
}

// Solicita a "Factory" que crie o objeto Automobile
$veyron = AutomobileFactory::create('Bugatti', 'Veyron');

print_r($veyron->get_make_and_model()); // imprime "Bugatti Veyron"
{% endhighlight %}

Esse código usa uma "Factory" para criar o objeto do tipo "Automobile". Existem dois possíveis benefícios para criar seu
código dessa forma, o primeiro é que se você precisar mudar, renomear ou substituir a classe Automobile futuramente você
pode fazer e só terá que modificar o código na "Factory", em vez de em todos os lugares do seu projeto onde você usa a
classe Automobile. O segundo benefício possível é que caso a criação do objeto seja um processo complicado, você
pode executar todo esse trabalho na factory, em vez de repetí-lo toda vez que precisar criar uma nova instância da classe.

Usar o padrão de "Factory" não é sempre necessário (ou esperto). O código de exemplo usado aqui é tão simples que essa
"Factory" estaria simplesmente adicionando complexidade indesejada. Entretanto se você estiver realizando um projeto um
pouco maior ou mais complexo você pode se salvar de muitos problemas com o uso do padrão "Factory".

* [Padrão "Factory" na Wikipedia](https://en.wikipedia.org/wiki/Factory_pattern)

## Singleton (Única Instancia)

Quando arquitetando uma aplicação web, é comum fazer sentido tanto conceitualmente quanto arquitetonicamente permitir o
acesso a somente uma instância de uma classe em particular, o padrão "Singleton" nos permite realizar essa tarefa.

{% highlight php %}
<?php
class Singleton
{
    /**
     * Retorna uma instância única de uma classe.
     *
     * @staticvar Singleton $instance A instância única dessa classe.
     *
     * @return Singleton A Instância única.
     */
    public static function getInstance()
    {
        static $instance = null;
        if (null === $instance) {
            $instance = new static();
        }

        return $instance;
    }

    /**
     * Construtor do tipo protegido previne que uma nova instância da
     * Classe seja criada através do operador `new` de fora dessa classe.
     */
    protected function __construct()
    {
    }

    /**
     * Método clone do tipo privado previne a clonagem dessa instância
     * da classe
     *
     * @return void
     */
    private function __clone()
    {
    }

    /**
     * Método unserialize do tipo privado para prevenir a desserialização
     * da instância dessa classe.
     *
     * @return void
     */
    private function __wakeup()
    {
    }
}

class SingletonChild extends Singleton
{
}

$obj = Singleton::getInstance();
var_dump($obj === Singleton::getInstance());             // bool(true)

$anotherObj = SingletonChild::getInstance();
var_dump($anotherObj === Singleton::getInstance());      // bool(false)

var_dump($anotherObj === SingletonChild::getInstance()); // bool(true)
{% endhighlight %}

O código acima implementa o padrão "Singleton" usando uma [variável *estática*](http://php.net/language.variables.scope#language.variables.scope.static)
e o método estático de criação `getInstance()`.
Note o seguinte:

* O construtor [`__construct`](http://php.net/language.oop5.decon#object.construct) é declarado como protegido para prevenir que uma nova instância seja criada fora dessa classe pelo operador `new`.
* O método mágico [`__clone`](http://php.net/language.oop5.cloning#object.clone) é declarado como privado para prevenir a clonagem dessa instância da classe pelo operador [`clone`](http://php.net/language.oop5.cloning).
* O método mágico [`__wakeup`](http://php.net/language.oop5.magic#object.wakeup) é declarado como privado para prevenir a desserialização de uma instância dessa classe pela função global [`unserialize()`](http://php.net/function.unserialize).
* Uma nova instância é criada via [late static binding](http://php.net/language.oop5.late-static-bindings) no método de criação `getInstance()` declarado como estático. Isso permite a criação de classes "filhas" da classe Singleton no exemplo

O padrão Singleton é útil quando você precisa garantir que somente uma instância da classe seja criada em todo o ciclo
de vida da requisição em uma aplicação web. Isso tipicamente ocorre quando você tem objetos globais (tais como uma
classe de Configuração) ou um recurso compartilhado (como uma lista de eventos).

Você deve ser cauteloso quando for usar o padrão "Singleton" já que pela sua própria natureza ele introduz um estado
global na sua aplicação reduzindo a possibilidade de realização de testes. Na maioria dos casos Injeção de Dependências
pode (e deve) ser usado no lugar de uma classe do tipo Singleton. Usar Injeção de Dependências significa não introduzir
acoplamento desnecessário no design da sua aplicação, já que o objeto usando o recurso global ou compartilhado não
necessita de conhecimento sobre uma classe concretamente definida.

* [Padrão Singleton na Wikipedia](https://en.wikipedia.org/wiki/Singleton_pattern)

## Strategy (Estratégia)

Com o padrão "Strategy" (Estratégia) voce encapsula famílias específicas de algoritimos permitindo com que a classe
cliente responsável por instanciar esse algoritimo em particular não necessite de conhecimento sobre sua implementação
atual. Existem várias variações do padrão "Strategy" o mais simples deles é apresentado abaixo:

O primeiro bloco de código apresenta uma familia de algorítimos; você pode querer uma array serializado, um JSON ou
talvez somente um array de dados:
{% highlight php %}
<?php

interface OutputInterface
{
    public function load();
}

class SerializedArrayOutput implements OutputInterface
{
    public function load()
    {
        return serialize($arrayOfData);
    }
}

class JsonStringOutput implements OutputInterface
{
    public function load()
    {
        return json_encode($arrayOfData);
    }
}

class ArrayOutput implements OutputInterface
{
    public function load()
    {
        return $arrayOfData;
    }
}
{% endhighlight %}

Através do encapsulamento do algoritimo acima você está fazendo seu código de forma limpa e clara para que outros
desenvolvedores possam facilmente adicionar novos tipos de saída sem que isso afete o código cliente.

Você pode ver como cada classe concreta 'output' implementa a OutputInterface - isso serve a dois propósitos,
primeiramente isso prevê um simples contrato que precisa ser obedecido por cada implementação concreta. Segundo, através
da implementação de uma interface comum você verá na próxima seção que você pode utilizar [Indução de Tipo](http://php.net/language.oop5.typehinting) para garantir que  o cliente que está utilizando esse comportamento é do tipo correto, nesse caso 'OutputInterface'.

O próximo bloco de código demonstra como uma classe cliente relizando uma chamada deve usar um desses algorítimos e
ainda melhor definir o comportamento necessário em tempo de execução:
{% highlight php %}
<?php
class SomeClient
{
    private $output;

    public function setOutput(OutputInterface $outputType)
    {
        $this->output = $outputType;
    }

    public function loadOutput()
    {
        return $this->output->load();
    }
}
{% endhighlight %}

A classe cliente tem uma propriedade private que deve ser definida em tempo de execução e ser do tipo 'OutputInterface'
uma vez que essa propriedade é definida uma chamada a loadOutput() irá chamar o método load() na classe concreta do tipo
'output' que foi definida.
{% highlight php %}
<?php
$client = new SomeClient();

// Quer um array?
$client->setOutput(new ArrayOutput());
$data = $client->loadOutput();

// Quer um JSON?
$client->setOutput(new JsonStringOutput());
$data = $client->loadOutput();

{% endhighlight %}

* [Padrão "Strategy" na Wikipedia](http://en.wikipedia.org/wiki/Strategy_pattern)

## Front Controller

O padrão front controller é quando você tem um único ponto de entrada para sua aplicação web (ex. index.php) que trata
de todas as requisições. Esse código é responsável por carregar todas as dependências, processar a requisição e enviar
a resposta para o navegador. O padrão Front Controller pode ser benéfico pois ele encoraja o desenvolvimento de um
código modular e provê um ponto central no código para inserir funcionalidades que deverão ser executadas em todas as
requisições (como para higienização de entradas).

* [Padrão Front Controller na Wikipedia](https://en.wikipedia.org/wiki/Front_Controller_pattern)

## Model-View-Controller

O padrão model-view-controller (MVC) e os demais padrões relacionados como HMVC e MVVM permitem que você separe o
código em diferentes objetos lógicos que servem para tarefas bastante específicas. Models (Modelos) servem como uma
camada de acesso aos dados onde esses dados são requisitados e retornados em formatos nos quais possam ser usados
no decorrer de sua aplicação. Controllers (Controladores) tratam as requisições, processam os dados retornados dos
Models e carregam as views (Visões) para enviar a resposta. E as views são templates de saída (marcação, xml, etc) que
são enviadas como resposta ao navegador.

O MVC é o padrão arquitetônico mais comumente utilizado nos populares [Frameworks PHP](https://github.com/codeguy/php-the-right-way/wiki/Frameworks).

Leia mais sobre o padrão MVC e os demais padrões relacionados:

* [MVC](https://en.wikipedia.org/wiki/Model%E2%80%93View%E2%80%93Controller)
* [HMVC](https://en.wikipedia.org/wiki/Hierarchical_model%E2%80%93view%E2%80%93controller)
* [MVVM](https://en.wikipedia.org/wiki/Model_View_ViewModel)
