---
isChild: true
title: Templates Simples em PHP
anchor: plain_php_templates
---

## Templates Simples em PHP {#plain_php_templates_title}

Templates Simples em PHP são templates que usam código nativo do PHP. Eles são uma escolha natural já que o PHP é na 
realidade um linguagem de template por si só. Isso significa simplesmente que você pode combinar código PHP dentro de 
outro código, como HTML. Isso é benéfico para os desenvolvedores de PHP pois não há uma nova sintaxe para aprender, 
eles sabem as funções disponíveis e seus editores de código PHP já tem syntax highlighting e auto-completion
embutidos. Além disso, estes templates tendem a ser muito mais rápido já que não é necessária a fase de compilação.

Cada framework moderno PHP emprega algum tipo de sistema de templates, a maioria usam PHP simples por padrão. Fora dos 
frameworks, bibliotecas como [Plates](http://platesphp.com/) ou [Aura.View](https://github.com/auraphp/Aura.View) 
tornam o trabalho mais fácil, oferecendo funcionalidade modernas ao template, tais como herança, layouts e extensões.

### Exemplo de um template simples em PHP

Utilizando a biblioteca [Plates](http://platesphp.com/).

{% highlight php %}
<?php // user_profile.php ?>

<?php $this->insert('header', ['title' => 'User Profile']) ?>

<h1>User Profile</h1>
<p>Hello, <?=$this->escape($name)?></p>

<?php $this->insert('footer') ?>
{% endhighlight %}

### Exemplo de um template simples em PHP usando herança

Utilizando a biblioteca [Plates](http://platesphp.com/).

{% highlight php %}
<?php // template.php ?>

<html>
<head>
    <title><?=$title?></title>
</head>
<body>

<main>
    <?=$this->section('content')?>
</main>

</body>
</html>
{% endhighlight %}

{% highlight php %}
<?php // user_profile.php ?>

<?php $this->layout('template', ['title' => 'User Profile']) ?>

<h1>User Profile</h1>
<p>Hello, <?=$this->escape($name)?></p>
{% endhighlight %}
