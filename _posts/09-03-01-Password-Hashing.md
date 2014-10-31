---
title: Hash de Senhas
isChild: true
anchor: hash_de_senhas
---

## Hash de Senhas {#hash_de_senhas_title}

No fim, todos construímos aplicações PHP que dependem de login dos usuários. Usuários e senhas (com hash) são
armazenadas em um banco de dados e posteriormente são usados para autenticar os usuários no login.

É importante que você faça adequadamente o [_hash_][3] das senhas que são armazenadas em um banco de dados.
Hash da senha é irreversível, uma função executada contra a senha do usuário. Isto produz uma seqüência
de comprimento fixo que não pode ser revertido. Isto significa que você pode comparar um hash contra o outro
para determinar se ambos foram produzidos da mesma string, mas você não pode determinar o string original.
Se as senhas não estiverm com hash, e seu banco for hackeado ou acessado por alguém não autorizado, todas as
contas dos usuários ficarão comprometidas. Alguns usuários (inflezmente) usam a mesma senha para outros
serviços. Por isso, é importante levar segurança a sério.

**Faça o hash das senhas com `password_hash`**

No PHP 5.5 `password_hash` foi adicionado. Neste momento utiliza o BCrypt, o mais forte algorítimo suportado
pelo PHP. Ele será atualizado no futuro para suportar mais algorítimos conforme for preciso.
A biblioteca `password_compat` foi criada para ter compatibilidade para o PHP >= 5.3.7.

Abaixo um exemplo, vamos fazer o hash de uma string, e em seguida, verificamos o hash contra uma nova string.
As duas string são diferentes ('secret-password' vs. 'bad-password') e por isso o login falhará.

{% highlight php %}
<?php

require 'password.php';

$passwordHash = password_hash('secret-password', PASSWORD_DEFAULT);

if (password_verify('bad-password', $passwordHash)) {
    //Senha correta
} else {
    //Senha Errada
}
{% endhighlight %}

* [Aprenda sobre `password_hash`] [1]
* [`password_compat` para PHP  >= 5.3.7 && < 5.5] [2]
* [Aprenda sobre hashing no que diz respeito à criptografia] [3]
* [PHP `password_hash` RFC] [4]

[1]: http://us2.php.net/manual/pt_BR/function.password-hash.php
[2]: https://github.com/ircmaxell/password_compat
[3]: http://en.wikipedia.org/wiki/Cryptographic_hash_function
[4]: https://wiki.php.net/rfc/password_hash