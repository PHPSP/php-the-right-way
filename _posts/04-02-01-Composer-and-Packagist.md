---
title: Composer e Packagist
isChild: true
anchor: composer_e_packagist
---

## Composer e Packagist {#composer_e_packagist_title}

O Composer é o gerenciador de dependências recomendado para PHP. Liste as dependências do seu projeto em um
arquivo `composer.json` e, com poucos comandos simples, o Composer irá fazer o download das dependências do seu
projeto automaticamente e configurará o autoloading para você. O Composer é semelhante ao NPM no mundo node.js ou o Bunder no mundo Ruby.

Já existem várias bibliotecas PHP que são compatíveis com o Composer, prontas para usar no seu projeto. Esses "pacotes"
estão listados no [Packagist], o repositório oficial das bibliotecas PHP compatíveis com o Composer.

### Como Instalar o Composer

A forma mais segura é fazer o download do composer [seguindo as instruções oficiais](https://getcomposer.org/download/). Isso vai verificar se o instalador não está corrompido ou foi adulterado.
O instalador instala um arquivo binário `composer.phar` no seu _diretório atual_.

Nós recomendadmos instalar o Composer *globally* (por exemplo uma única cópia no diretório `/usr/local/bin`). Para fazer isso, rode o próximo comando:

{% highlight console %}
mv composer.phar /usr/local/bin/composer
{% endhighlight %}

**Nota:** Se o comando falhar devido a permissão, use o comando `sudo` no início.

Para rodar o Composer instalado localmente, use o comando `php composer.phar`, e globalmente apenas `composer`.

#### Instalação no Windows

Para usuários Windows a forma mais fácil de obter e executá-lo é usar o instalador [ComposerSetup], que realiza uma 
instalação global e configura seu `$PATH` de modo que você possa executar o comando `composer` de qualquer diretório 
pela linha de comando. 

### Como Definir e Instalar Dependências

O Composer mantém o controle de dependências do seu projeto em um arquivo chamado `composer.json`. Você pode
controlá-lo na mão se preferir ou usar o próprio Composer. O comando `composer require` adiciona uma dependência do
projeto e se você não tem um arquivo `composer.json`, ele será criado. Aqui está um exemplo que adiciona
o [Twig] como uma dependência do seu projeto:

{% highlight console %}
composer require twig/twig:^2.0
{% endhighlight %}

Outra alternativa é o comando `composer init` que guiará a criação completa do arquivo `composer.json` para
seu projeto. De qualquer maneira, uma vez criado o arquivo `composer.json` você pode chamar o Composer para baixar suas
dependências para o diretório `vendor/`. Isto também se aplica para projetos baixados que fornecem um arquivo
`composer.json`:

{% highlight console %}
composer install
{% endhighlight %}

Em seguida, adicione esta linha ao arquivo PHP principal da sua aplicação; isso dirá ao PHP para usar o autoloader do
Composer para as dependências do seu projeto:

{% highlight php %}
<?php
require 'vendor/autoload.php';
{% endhighlight %}

Agora você pode usar as dependências do seu projeto, e elas serão carregadas automaticamente sob demanda.

### Atualizando suas dependências

O Composer cria um arquivo chamado `composer.lock` que armazena a versão exata de cada pacote baixado quando você
executou `composer install`. Se você compartilhar seu projeto com outras pessoas, certifique-se que o o arquivo `composer.lock` está incluído, pois quando eles executarem o comando `composer install` eles receberão as mesmas versões que você possui. Para atualizar suas dependências, execute o comando `composer update`. Não use o comando `composer update` quando estiver fazendo deploy, use apenas `composer install`, senão você poderá terminar com versões de pacotes diferentes em produção.

Isso é muito útil quando você define as versões requeridascom flexibilidade. Por exemplo, uma versão requerida de `~1.8` significa "qualquer versão mais recente que `1.8.0`, mas menos recente do que `2.0.x-dev`". Você também pode usar o curinga `*` como `1.8.*`.
Agora o comando `composer update` atualizará todas as suas dependências para a versão mais recente
que se encaixa às restrições definidas.

### Notificações de Atualização

Para receber notificações sobre novas versões você pode se inscrever no [libraries.io], um serviço web que pode
monitorar dependências e lhe enviar alertas de atualizações.

### Tratando dependências globais com Composer

O Composer também pode tratar dependências globais e seus binários. O seu uso é direto, tudo que você precisa é prefixar seu comando com a palavra `global`. Se por exemplo você quer instalar o PHPUnit e quer tê-lo disponível globalmente, você deve rodar o seguinte comando:

{% highlight console %}
composer global require phpunit/phpunit
{% endhighlight %}

Isso irá criar uma pasta `~/.composer` onde suas dependências globais residem. Para ter os pacotes binários disponíveis em qualquer lugar, você deve adicionar a pasta `~/.composer/vendor/bin` para sua variável `$PATH`.

* [Aprenda sobre o Composer][Learn about Composer]

[Packagist]: https://packagist.org/
[Twig]: https://twig.symfony.com/
[libraries.io]: https://libraries.io/
[Security Advisories Checker]: https://security.sensiolabs.org/
[Learn about Composer]: https://getcomposer.org/doc/00-intro.md
[ComposerSetup]: https://getcomposer.org/Composer-Setup.exe
