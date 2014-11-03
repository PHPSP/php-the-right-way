---
title: Cache de Objetos
isChild: true
anchor: cache_de_objetos
---

## Cache de Objetos {#cache_de_objetos_title}

Existem momentos onde pode ser benéfico fazer cache de objetos individuais no seu código, como em dados que são
custosos de conseguir ou em chamadas de bancos de dados cujo resultado dificilmente se modifica. Você pode usar um
software de cache de objetos para armazenar esses pedaços de dados na memória, para acessá-los posteriomente de forma
extremamente rápida. Se você guardar esses itens em um data store logo que os recuperar, e depois os enviar
diretamente do cache para as suas requisições posteriores, você conseguirá uma melhora significativa no desempenho
além de reduzir a carga nos seus servidores de banco de dados.

Muitas das soluções populares de cache de bytecode permitem que você também faça cache de dados personalizados, assim
há ainda mais razões para se beneficiar deles. Tanto o APC, quanto o XCache e o Wincache fornecem APIs para armazenar
dados do seu código PHP na memória cache deles.

Os sistemas mais usados para cache de objetos em memória são o APC e o memcached. O APC é uma escolha excelente para
cache de objetos, ele inclui uma API simples para adicionar seus próprios dados para seu cache de memória e é muito
fácil de configurar e utilizar. A única limitação real do APC é que ele fica amarrado ao servidor onde ele está
instalado. O memcached por outro lado é instalado como um serviço separado e pode ser acessado através da rede, assim
você pode armazenar objetos em um data store ultra-rápido, em uma localização central, e vários sistemas diferentes
podem acessá-lo.

Note que se estiver rodando o PHP como uma aplicação (Fast-)CGI dentro do seu servidor web, cada processo do PHP terá
seu próprio cache, ou seja, os dados de APCu não são compartilhados entre diferentes processos. Nesse caso você deve
considerar usar mecached em seu lugar, já que ele não está ligado aos processos do PHP.

Em uma configuração em rede, o APC geralmente terá um desempenho melhor do que o memcached em termos da velocidade de
acesso, mas o memcached poderá escalar mais rápido e melhor. Se você não planeja ter múltiplo servidores executando
sua aplicação, ou não precisar das funcionalidades extras que o memcached oferece, então o APC provavelmente é sua
melhor opção para cache de objetos.

Exemplo de lógica usando APC:

{% highlight php %}
<?php
// verifica se existe um dado salvo como 'expensive_data' no cache
$data = apc_fetch('expensive_data');
if (!$data)
{
    // dado não está no cache, faça a chamada custosa e guarde-a para usar depois
    $data = get_expensive_data();
    apc_store('expensive_data', $data);
}

print_r($data);
{% endhighlight %}

Note que, antes do PHP 5.5, APC possui tanto um cache de objetos quanto um cache de bytecode. APCu é um projeto que tem
como objetivo trazer o cache de objetos do APC para o PHP 5.5, já que o PHP agora possui um cache bytecode nativo
(OPcache).

Aprenda mais sobre sistemas populares de cache de objetos:

* [APCu](https://github.com/krakjoe/apcu)
* [Funções APC](http://php.net/manual/pt_BR/ref.apc.php)
* [Memcached](http://memcached.org/)
* [Redis](http://redis.io/)
* [XCache APIs](http://xcache.lighttpd.net/wiki/XcacheApi)
* [Funções do WinCache](http://www.php.net/manual/pt_BR/ref.wincache.php)
