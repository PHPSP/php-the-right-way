---
layout: page
title: Programação Funcional em PHP
---

# Programação Funcional em PHP

O PHP suporta funções de primeira classe, o que significa que uma função pode ser atribuída a uma variável. Ambas
definidas pelo usuário e as funções embutidas podem ser referenciadas como uma variável e invocadas dinamicamente.
As Funções podem ser passadas como argumentos para outras funções (um recurso chamado de funções de ordem-superior)
e uma função pode retornar outras funções.

Recursão, um recurso que permite uma função chamar ela mesma, é suportado pela linguagem, mas a maior parte do código
PHP é focado em iteração.

Funções Anônimas (com suporte para closures) estão presentes desde a versão 5.3 do PHP (2009).

No PHP 5.4+ foi adicionada a capacidade de atribuir closures no escopo de um objetos e também melhorou o suporte
para funções chamáveis de tal forma podem ser usadas como sinônimo de funções anônimas em quase todos os casos.

O uso mais comum de funções de ordem superior ocorre na implementação do padrão Estratégia (Strategy). A função embutida
`array_filter` pede a entrada de array (data) e uma função (uma estratégia ou um callback) usada como um filtro para
cada item do array.

{% highlight php %}
<?php
$input = array(1, 2, 3, 4, 5, 6);

// cria uma nova função anônima e atribui a uma variável
$filter_even = function($item) {
    return ($item % 2) == 0;
};

// constrói o array_filter com os dados e a função
$output = array_filter($input, $filter_even);

// a função não precisa ser atribuída a uma variável. Assim também é válido:
$output = array_filter($input, function($item) {
    return ($item % 2) == 0;
});

print_r($output);
{% endhighlight %}

Uma closure é uma função anônima que pode acessar variáveis importadas a partir de fora do escopo usando qualquer
variável global. Teoricamente, um closure é uma função com alguns argumentos fechados (por exemplo, fixo) pelo ambiente
quando é definido. Closures podem contornar restrições de escopo de variáveis de uma maneira simples.

No próximo exemplo, usamos closures para definir uma função que retorna um filtro único para `array_filter`, fora
da família de funções de filtro.

{% highlight php %}
<?php
/**
 * Cria uma função de filtro anônima que aceita $items > $min
 *
 * Retorna um único filtro fora da família de filtros "maior que n"
 */
function criteria_greater_than($min)
{
    return function($item) use ($min) {
        return $item > $min;
    };
}

$input = array(1, 2, 3, 4, 5, 6);

// Utiliza array_filter em uma entrada com uma função de filtro selecionada
$output = array_filter($input, criteria_greater_than(3));

print_r($output); // itens > 3
{% endhighlight %}

Cada função de filtro na família aceita apenas elementos maiores que algum valor mínimo. Único filtro retornado pela
`criteria_greater_than` é um closure com o argumento `$min` pelo valor no escopo (dado como um argumento quando
`criteria_greater_than` é chamada).

A vinculação antecipada é usada por padrão para a importação da variável `$min`dentro da função criada. Para
verdadeiras closures com uma vinculação posterior deve ser usada uma referência quando importar. Imagine um template ou
uma biblioteca de validação, onde o closure é definido para capturar variáveis no escopo e acessá-los mais tarde quando
a função anônima for compilada.

* [Leia sobre Funções Anônimas][anonymous-functions]
* [Mais detalhes em Closures RFC][closures-rfc]
* [Leia sobre invocar dinamicamente funções com `call_user_func_array`][call-user-func-array]

[anonymous-functions]: http://www.php.net/manual/pt_BR/functions.anonymous.php
[call-user-func-array]: http://php.net/manual/pt_BR/function.call-user-func-array.php
[closures-rfc]: https://wiki.php.net/rfc/closures
