---
layout: page
title: The Basics
---

# O Básico

## Operadores de Comparação

Operadores de Comparação são frequentemente negligenciados em PHP, o que pode levar a muitos resultados inesperados. Um
desses problemas decorre de comparações estritas (comparações entre booleanos e inteiros).

{% highlight php %}
<?php
$a = 5;   // 5 como inteiro

var_dump($a == 5);       // comparação de valores; retorna true
var_dump($a == '5');     // comparação de valores (ignorando os tipos); retorna true
var_dump($a === 5);      // comparação de tipos e valores (integer vs. integer); retorna true
var_dump($a === '5');    // comparação de tipos e valores (integer vs. string); retorna false

/**
 * Comparações Estritas
 */
if (strpos('testing', 'test')) {    // 'test' é encontrado na posição 0, que é interpretado como o booleano 'false'
    // código...
}

vs.

if (strpos('testing', 'test') !== false) {    // true, já que uma comparação estrita foi feita (0 !== false)
    // código...
}
{% endhighlight %}

* [Operadores de Comparação](http://php.net/manual/pt_BR/language.operators.comparison.php)
* [Tabela de Comparação](http://php.net/manual/pt_BR/types.comparisons.php)

## Estrutura de Controle

### Estruturas Condicionais

Quando as declarações 'if/else' são usadas em uma função ou classe, é um equívoco comum pensar que 'else' precisa ser
usado em conjunto para declarar resultados em potencial. Entretanto se o resultado serve para definir o valor a ser
retornado 'else' não é necessário já que 'return' irá terminar a função, fazendo com que o uso de 'else' se torne
discutível.

{% highlight php %}
<?php
function test($a)
{
    if ($a) {
        return true;
    } else {
        return false;
    }
}

vs.

function test($a)
{
    if ($a) {
        return true;
    }
    return false;    // else não é necessário
}
{% endhighlight %}

* [Estrutura Condicionais](http://php.net/manual/pt_BR/control-structures.if.php)

### Estruturas de Decisão

Estruturas de decisão são uma excelente forma de evitar escrever intermináveis estruturas condicionais, mas existem
alguns pontos sobre os quais deve-se ficar atento:

- Estruturas de decisão só comparam valores, e não tipos (equivalente a '==')
- Elas passam por caso a caso até que uma correspondencia seja encontrada, então default é usado (caso esteja definido)
- Sem que haja um 'break', elas continuarão a executar cada caso até que encontrem um break/return
- Dentro de uma função o uso de 'return' remove a necessidade do uso de 'break' já que isso encerra essa função

{% highlight php %}
<?php
$answer = test(2);    // tanto o código para o 'case 2' quanto para o 'case 3' será executado

function test($a)
{
    switch ($a) {
        case 1:
            // código...
            break;             // break é usado para terminar a estrutura de decisão
        case 2:
            // código...         // sem o break, a comparação ira continuar em 'case 3'
        case 3:
            // código...
            return $result;    // dentro de uma função, 'return' termina essa função
        default:
            // código...
            return $error;
    }
}
{% endhighlight %}

* [Estruturas de Decisão](http://php.net/manual/pt_BR/control-structures.switch.php)
* [PHP Switch](http://phpswitch.com/)

## Namespace Global

Quando estiver usando namespaces você pode reparar que funções internas ficam escondidas por funções que você mesmo
escreveu. Para corrigir isso refira a funções globais através do uso de uma contra-barra antes do nome da função.

{% highlight php %}
<?php
namespace phptherightway;

function fopen()
{
    $file = \fopen();    // O nome da nossa função é igual a de uma função interna.
                         // Execute a função global através da inclusão de '\'.
}

function array()
{
    $iterator = new \ArrayIterator();    // ArrayIterator é uma classe interna. Usar seu nome sem uma contra-barra
                                         // tentará localizar essa função dentro do namespace
}
{% endhighlight %}

* [Espaço Global](http://php.net/manual/pt_BR/language.namespaces.global.php)
* [Regras Globais](http://php.net/manual/pt_BR/userlandnaming.rules.php)

## Strings

### Concatenação

- Se sua linha passar do tamanho recomendado (120 caracteres), considere concatenar sua linha
- Para facilitar a leitura é melhor usar operadores de concatenação do que operadores de concatenação e atribuição
- Enquanto dentro do escopo original da variável, indente quando a concatenação usar uma nova linha


{% highlight php %}
<?php
$a  = 'Multi-line example';    // operador de concatenação e atribuição (.=)
$a .= "\n";
$a .= 'of what not to do';

vs.

$a = 'Multi-line example'      // operador de concatenação (.)
    . "\n"                     // indentando novas linhas
    . 'of what to do';
{% endhighlight %}

* [Operadores de Strings](http://php.net/manual/pt_BR/language.operators.string.php)

### Tipos de Strings

Tipos de string são uma característica constante na comunidade PHP, mas talvez essa seção possa explicar as diferenças
entre os tipos de strings e seus usos e benefícios.

#### Aspas Simples

Usar aspas simples é o melhor jeito de definir strings e geralmente também o mais rápido. Sua velocidade se dá ao fato
do PHP não tentar interpretar essa string (suas variáveis). É a melhor aplicação quando:

- Strings não precisam ser interpretadas
- Uma variável é escrita em texto plano

{% highlight php %}
<?php
echo 'Essa é minha string, veja como ela é bonita.';    // sem necessidade de interpretar uma string simples

/**
 * Saída:
 *
 * Essa é minha string, veja como ela é bonita.
 */
{% endhighlight %}

* [Aspas Simples](http://www.php.net/manual/pt_BR/language.types.string.php#language.types.string.syntax.single)

#### Aspas Duplas

Aspas Duplas são o canivete suíço das strings, mas são mais lentas devido a interpretação das strings. É a melhor
aplicação quando:

- Escapando strings
- Usando strings com muitas variáveis e texto plano
- Condensando concatenação de múltiplas linhas e aumentando a legibilidade

{% highlight php %}
<?php
echo 'phptherightway é ' . $adjective . '.'      // Um exemplo com aspas simples que usa concatenação múltipla para
    . "\n"                                       // variáveis e escapar strings
    . 'Eu amo aprender' . $code . '!';

vs.

echo "phptherightway is $adjective.\n Eu amo aprender $code!"  // Em vez de concatenação múltipla, aspas duplas
                                                               // nos permitem utilizar strings interpretáveis
{% endhighlight %}

Quando strings em aspas duplas que contenham variáveis, são comuns os casos onde a variável pode estar colada com outro
caracter. Isso fará com que o PHP não consiga interpretar essa variável pelo fato dela estar sendo camuflada. Para
corrigir esse problema envolva a variável em um par de chaves.

{% highlight php %}
<?php
$juice = 'ameixa';
echo "Eu bebi suco feito de $juices";    // $juice não pode ser interpretado

vs.

$juice = 'ameixa';
echo "Eu bebi suco feito de {$juice}s";    // $juice será interpretado

/**
 * Variáveis complexas também serão interpretadas com o uso de chaves
 */

$juice = array('maça', 'laranja', 'ameixa');
echo "Eu bebi suco feito de {$juice[1]}s";   // $juice[1] será interpretado
{% endhighlight %}

* [Aspas Duplas](http://www.php.net/manual/pt_BR/language.types.string.php#language.types.string.syntax.double)

#### Sintaxe Nowdoc

A Sintaxe Nowdoc foi introduzida no PHP 5.3 e internamente se comporta da mesma forma que as aspas simples exceto que é
adequada para o uso de strings de múltiplas linhas sem a necessidade de concatenação.

{% highlight php %}
<?php
$str = <<<'EOD'             // iniciada por <<<
Exemplo de string
pulando multiplas linhas
usando a sintaxe nowdoc.
$a não é interpretada.
EOD;                        // fechando 'EOD' precisa estar na sua própria linha, e no ponto mais a esquerda

/**
 * Saída:
 *
 * Exemplo de string
 * pulando múltiplas linhas
 * usando a sintaxe nowdoc.
 * $a não é interpretada.
 */
{% endhighlight %}

* [Sintaxe Nowdoc](http://www.php.net/manual/pt_BR/language.types.string.php#language.types.string.syntax.nowdoc)

#### Sintaxe Heredoc

A Sintaxe Heredoc se comporta internamente da mesma forma que as aspas duplas exceto que é adequada para o uso de strings
de múltiplas linhas sem a necessidade de concatenação.

{% highlight php %}
<?php
$a = 'Variáveis';

$str = <<<EOD               // initialized by <<<
Exemplo de string
pulando múltiplas linhas
usando a sintaxe heredoc.
$a são interpretadas.
EOD;                        // closing 'EOD' must be on it's own line, and to the left most point

/**
 * Output:
 *
 * Exemplo de string
 * pulando múltiplas linhas
 * usando a sintaxe heredoc.
 * variáveis são interpretadas.
 */
{% endhighlight %}

* [Sintaxe Heredoc](http://www.php.net/manual/pt_BR/language.types.string.php#language.types.string.syntax.heredoc)

## Operadores Ternários

O uso de operadores ternários é uma ótima forma de condensar seu código, mas eles são geralmente usados em excesso.
Apesar de operações ternárias poderem ser agrupadas e aconselhado usar uma por linha para aumentar a legibilidade.

{% highlight php %}
<?php
$a = 5;
echo ($a == 5) ? 'yay' : 'nay';

vs.

// operações ternárias agrupadas
$b = 10;
echo ($a) ? ($a == 5) ? 'yay' : 'nay' : ($b == 10) ? 'excessive' : ':(';    // excesso de agrupamento sacrifica a legibilidade
{% endhighlight %}

Para usar 'return' em um operador ternário utilize a sintaxe correta.

{% highlight php %}
<?php
$a = 5;
echo ($a == 5) ? return true : return false;    // esse exemplo irá disparar um erro

vs.

$a = 5;
return ($a == 5) ? 'yay' : 'nope';    // esse exemplo irá retornar 'yay'
{% endhighlight %}

* [Operadores Ternários](http://php.net/manual/pt_BR/language.operators.comparison.php)

## Declaração de Variáveis

As vezes  programadores tentam tornar seu código mais limpo declarando variáveis predefinidas com um nome diferente. O
que isso faz na realidade e dobrar o consumo de memória do script. No exemplo abaixo, digamos que uma string de exemplo
contém 1MB de dado válido, copiando a variável você aumenta o consumo de memória durante a execução para 2MB.

{% highlight php %}
<?php
$about = 'Uma string com texto bem longo';    // usa 2MB de memória
echo $about;

vs.

echo 'Uma string com texto bem longo';        // usa 1MB de memória
{% endhighlight %}

* [Dicas de Performance](https://developers.google.com/speed/articles/optimizing-php)
