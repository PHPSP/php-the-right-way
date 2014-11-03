---
title: Namespaces
isChild: true
anchor: namespaces
---

## Namespaces {#namespaces_title}

Como mencionado anteriormente, a comunidade PHP tem muitos desenvolvedores criando muito código. Isso significa que o
código de uma biblioteca PHP pode usar o mesmo nome de classe que uma outra biblioteca. Quando ambas bibliotecas são
usadas no mesmo namespace, elas colidem e causam problemas.

Os _Namespaces_ resolvem esse problema. Como descrito no manual de referência do PHP, os namespaces podem ser
comparados com os diretórios dos sistemas operacionais, que fazem _namespace_ dos arquivos; dois arquivos com o mesmo
nome podem coexistir em diretórios separados. Da mesma forma, duas classes PHP com o mesmo nome podem coexistir em
namespaces PHP separados. Simples assim.

É importante que você use namespace no seu código para que ele possa ser usado por outros desenvolvedores sem risco
de colisão com outras bibliotecas.

Um modo recomendado de usar namespaces está descrito na [PSR-0][psr0], que tem como objetivo fornecer uma convenção
padrão para arquivos, classes e namespaces, permitindo código plug-and-play.

* [Leia sobre os Namespaces][namespaces]
* [Leia sobre a PSR-0][psr0]

[namespaces]: http://php.net/manual/pt_BR/language.namespaces.php
[psr0]: https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-0.md
