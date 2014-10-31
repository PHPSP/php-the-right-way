---
title: Exceções
isChild: true
anchor: excecoes
---

## Exceções {#excecoes_title}

Exceções são uma parte padrão da maioria das linguagens populares, mas elas sao frequentemente negligenciadas pelos
programadores de PHP. Linguagens como Ruby usam pesadamente o sistema de Exceções, então sempre que algo de errado
acontece, como um pedido HTTP que falha, ou uma consulta ao banco de dados gera um erro, ou até mesmo se uma imagem
não puder ser encontrada, o Ruby (ou suas bibliotecas que estiverem sendo utilizadas) irão disparar uma exceção para
a tela, assim você saberá imediatamente que algo está errado.

O PHP por si só é bastante relaxado com isso, e uma chamada para `file_get_contents()` irá resultar apenas em um `FALSE`
e um alerta. Muitos frameworks antigos, como CodeIgniter, irão apenas retornar um `FALSE`, registrar
uma mensagem em seus logs proprietários e talvez deixar que você use um método como `$this->upload->get_error()` para
ver o que houve de errado. O problema, aqui, é você tem que sair procurando por um erro e verificar na documentação para
saber como achar o método que retorna o erro para essa classe, em vez de ter isso de forma extremamente óbvia.

Outro problema é quando as classes automaticamente disparam um erro para a tela e finalizam o processo. Quando você
faz isso você impede que outro programador seja capaz de dinamicamente lidar com o erro. Exceções devem ser disparadas
para que os desenvolvedores fiquem a par do erro, para então decidirem como lidar com ele. Ex:

{% highlight php %}
<?php
$email = new Fuel\Email;
$email->subject('My Subject');
$email->body('How the heck are you?');
$email->to('guy@example.com', 'Some Guy');

try
{
    $email->send();
}
catch(Fuel\Email\ValidationFailedException $e)
{
    // The validation failed
}
catch(Fuel\Email\SendingFailedException $e)
{
    // The driver could not send the email
}
{% endhighlight %}

### SPL Exceptions

Por padrão uma exceção não tem significado nenhum, e a forma mais comum de dar um significado é pela definição do seu
próprio nome:

{% highlight php %}
<?php
class ValidationException extends Exception {}
{% endhighlight %}

Isso significa que você pode adicionar múltiplos blocos de captura para lidar com diferentes Exceções. Isso pode lhe
levar a criação de <em>muitas</em> exceções customizadas, e algumas delas poderiam ter sido evitadas como o uso das
SPL Exceptions (exceções da biblioteca padrão) que estão disponíveis em [SPL extension][splext].

Se por exemplo você fizer uso do método mágico `__call()` e o método chamado for inválido, então em vez de disparar
uma exceção padrão que seria muito vaga, ou criar uma exceção apenas para isso, você poderia disparar apenas um
`throw new BadFunctionCallException;`.

* [Leia sobre Exceções][exceptions]
* [Leia sobre SPL Exceptions][splexe]
* [Aninhando exceções no PHP][nesting-exceptions-in-php]
* [Melhores práticas com exceções no PHP 5.3][exception-best-practices53]

[exceptions]: http://php.net/manual/pt_BR/language.exceptions.php
[splexe]: http://php.net/manual/pt_BR/spl.exceptions.php
[splext]: /#standard_php_library
[exception-best-practices53]: http://ralphschindler.com/2010/09/15/exception-best-practices-in-php-5-3
[nesting-exceptions-in-php]: http://www.brandonsavage.net/exceptional-php-nesting-exceptions-in-php/
