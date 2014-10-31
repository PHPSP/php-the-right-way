---
title: Cache de Bytecode
isChild: true
anchor: cache_de_bytecode
---

## Cache de Bytecode {#cache_de_bytecode_title}

Quando um arquivo PHP é executado, por baixo dos panos ele primeiro é compilado para bytecode (também conhecido como
opcode) e, só aí, o bytecode é executado.  Se o arquivo PHP não foi modificado, o bytecode será sempre o mesmo. Isso
significa que o passo de compilação é um desperdício de recursos de CPU.

É aqui que entra o cache de Bytecode. Ele previne as compilações redundantes armazenando bytecode na memória e
reutilizando-o em chamadas sucessivas. A configuração do cache de bytecode é feita em questão de minutos, e sua
aplicação irá acelerar de forma significativa. Não existe razão para não utilizá-lo.

No PHP 5.5 o OPcache foi incluído como um cache de bytecode nativo. Ele também está disponível para versões anteriores.

Caches de bytecode populares são:

* [APC](http://php.net/manual/pt_BR/book.apc.php)  (PHP 5.4 e anteriores)
* [XCache](http://xcache.lighttpd.net/)
* [Zend Optimizer+](http://www.zend.com/products/server/) (parte do pacote Zend Server)
* [WinCache](http://www.iis.net/download/wincacheforphp) (extensão para o MS Windows Server)
