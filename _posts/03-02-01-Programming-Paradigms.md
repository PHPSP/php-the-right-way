---
title: Paradigmas de programação
isChild: true
anchor: paradigmas_de_programacao
---

## Paradigmas de programação {#paradigmas_de_programacao_title}

O PHP é uma linguagem dinâmica e flexível, que suporta uma variedade de técnicas de programação. Ele evoluiu
drasticamente com o passar dos anos, notavelmente adicionando um sólido modelo de orientação a objetos no PHP 5.0 
2004), funções anônimas e namespaces no PHP 5.3 (2009) e traits no PHP 5.4 (2012).

### Programação orientada a objetos

O PHP possui um conjunto completo de funcionalidades de programação orientada a objetos, incluindo suporte à classes,
classes abstratas, interfaces, herança, construtores, clonagem, exceções e muito mais.

* [Leia sobre PHP orientado a objetos][oop]
* [Leia sobre Traits][traits]

### Programação funcional

PHP suporta funções de primeira classe, o que significa que funções podem ser atribuidas a variáveis. Tanto funções
nativas como funções definidas por usuários podem ser referenciadas por uma variável e invocadas dinamicamente. Funções
também pode ser passadas como argumentos para outras funções (funcionalidade chamada de funções de ordem superior) e
funções podem retornar outras funções.

Recursão, uma funcionalidade que permite que funções realizem chamadas para elas mesmas também é suportada pela
linguagem, mas a maioria dos códigos em PHP tem foco em iteração.

Novas funções anônimas (incluindo suporte para closures) também estão presentes de o PHP 5.3 (2009).

PHP 5.4 inclui a habilidade de vincular closures com o escopo de objetos e também melhorou o suporte para invocaveis
(callables) tanto que elas podem ser usadas indistintamente com funções anónimas na maioria dos casos.

* Continue lendo em [Programação Funcional em PHP](/pages/Functional-Programming.html)
* [Leia mais sobre Funções Anônimas][anonymous-functions]
* [Leia mais sobre Closures][closure-class]
* [Mais detalhes na RFC sobre Closures][closures-rfc]
* [Leia mais sobre invocáveis (callables)][callables]
* [Leia sobre invocamento dinâmico de funções com `call_user_func_array`][call-user-func-array]

### Meta Programação

PHP suporta varias formas de meta-programação através de mecanismos como a API de reflexão e métodos mágicos. Existem
vários métodos mágicos disponíveis como __get(), __set(), __clone(), __toString(), __invoke(), etc. Isso permite que
desenvolvedores alterem o comportamento das classes. Desenvolvedores Ruby costumam dizer que o PHP carece de
`method_missing`, mas ele está disponível com `__call()` e __callStatic().

* [Leia sobre Métodos Mágicos][magic-methods]
* [Leia sobre Reflexão][reflection]

[namespaces]: http://php.net/manual/pt_BR/language.namespaces.php
[overloading]: http://php.net/manual/pt_BR/language.oop5.overloading.php
[oop]: http://www.php.net/manual/pt_BR/language.oop5.php
[anonymous-functions]: http://www.php.net/manual/pt_BR/functions.anonymous.php
[closure-class]: http://php.net/manual/pt_BR/class.closure.php
[callables]: http://php.net/manual/en/language.types.callable.php
[magic-methods]: http://php.net/manual/pt_BR/language.oop5.magic.php
[reflection]: http://www.php.net/manual/pt_BR/intro.reflection.php
[traits]: http://br1.php.net/traits
[call-user-func-array]: http://php.net/manual/pt_BR/function.call-user-func-array.php
[closures-rfc]: https://wiki.php.net/rfc/closures
