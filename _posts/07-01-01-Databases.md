---
title: Banco de Dados
anchor: banco_de_dados
---

# Bancos de Dados {#banco_de_dados_title}

Muitas vezes o seu código PHP usará um banco de dados para persistir informações. Você tem algumas opções para
conectar e interagir como seu banco de dados. A opção recomendada _até o PHP 5.1.0_ era usar os drivers nativos, como
o [mysql][mysql], o [mysqli][mysqli], o [pgsql][pgsql] etc.

Drivers nativos são excelentes se você estiver usando apenas UM banco de dados na sua aplicação, mas se, por exemplo,
você estiver usando o MySQL e um pouco de MSSQL, ou você precisar conectar em um banco de dados Oracle, aí você não
poderá usar os mesmos drivers. Você precisará aprender um API totalmente nova para cada um dos bancos de dados &mdash;
e isso pode ficar chato.

Uma observação adicional sobre os drivers nativos: a extensão mysql para o PHP não está mais em desenvolvimento ativo
, e a situação oficial desde o PHP 5.4.0 é "Long term deprecation", ou "Obsoleta no longo prazo". Isso significa que
ela será removida dentro de alguns lançamentos das próximas versões, assim, por volta do PHP 5.6 (ou o que venha
depois do 5.5), ela pode muito bem ter desaparecido. Se você estiver usando `mysql_connect()` e `mysql_query()` nas
suas aplicações você irá se deparar com uma reescrita em algum momento no futuro, por isso a melhor opção é
substituir o uso do mysql pelo mysqli ou pela PDO na sua aplicação dentro de sua própria agenda de desenvolvimento,
assim você não terá que correr lá na frente. _Se você estiver começando do zero então não utilize de forma nenhuma a
extensão mysql: use a [extensão MySQLi][mysqli], ou use a PDO._

* [PHP: Choosing an API for MySQL](http://php.net/manual/pt_BR/mysqlinfo.api.choosing.php)

## PDO

A PDO é uma biblioteca para abstração de conexões a bancos de dados &mdash; embutida no PHP desde a versão 5.1.0 
&mdash; que fornece uma interface comum para conversar com vários bancos de dados diferentes. A PDO não irá traduzir
suas consultas SQL ou emular funcionalidades que não existem; ela é feita puramente para conectar múltiplos tipos de
bancos de dados com a mesma API.

Mais importante, a `PDO` permite que você injete de forma segura entradas externas (e.g IDs) em suas consultas SQL
sem se preocupar com ataques de SQL injection.  Isso é possível usando instruções PDO (PDO statements) e parâmetros
restritos (bound parameters).

Vamos assumir que um script PHP recebe um ID numérico como parâmetro de uma consulta. Esse ID deve ser usado para
buscar um registro de um usuário no banco de dados. Essa é a forma `errada` de fazer isso:

{% highlight php %}
<?php
$pdo = new PDO('sqlite:users.db');
$pdo->query("SELECT name FROM users WHERE id = " . $_GET['id']); // <-- NO!
{% endhighlight %}

Esse código é péssimo. Você está inserindo um parâmetro bruto na sua consulta SQL. Isso fará você ser hackeado num
piscar de olhos. Apenas imagine se um hacker passar como parâmetro um `id` criativo chamando uma URL como
`http://domain.com/?id=1%3BDELETE+FROM+users`. Isso irá definir a variável `$_GET['id']` como `id=1;DELETE FROM users`,
o que irá excluir todos os seus usuários. Em vez disso, você deveria higienizar (sanitize) a entrada do ID usando
parâmetros restritos da PDO.

{% highlight php %}
<?php
$pdo = new PDO('sqlite:users.db');
$stmt = $pdo->prepare('SELECT name FROM users WHERE id = :id');
$stmt->bindParam(':id', $_GET['id'], PDO::PARAM_INT); //<-- Higienizado automaticamente sanitized pela PDO
$stmt->execute();
{% endhighlight %}

Esse é o código correto. Ele usa um parâmetro restrito em uma instrução PDO. Assim a entrada externa do ID é escapada
antes de ser introduzida no banco de dados, prevenindo contra potenciais ataques de SQL injection.

* [Leia sobre a PDO][1]

Você também deve estar ciente de que usam recursos do servidor e não é raro ter esses recursos esgotados se essas
conexões não forem implicitamente fechadas, entretanto isso é mais comum em outras linguagens. Com PDO você pode
implicitamente fechar as conexões pela destruição dos objetos garantindo que todas as referências a ele forem excluídas,
ex. atribuindo NULL a elas. Se você não fizer isso explicitamente o PHP irá fechar todas as conexões quando seu script
terminar, a não ser é claro que você esteja usando conexões persistentes.

* [Leia mais sobre conexões PDO][5]

## Camadas de Abstração

Muitos frameworks fornecem sua própria camada de abstração que pode ou não ser baseada na PDO. Elas frequentemente
irão emular funcionalidades de um sistema de banco de dados que não estão presentes nos outros, embutindo suas
consultas SQL em métodos PHP, te dando abstração real de banco de dados.  Isso, naturalmente, adiciona uma pequena
sobrecarga, mas se você estiver construindo uma aplicação portátil que precise trabalhar com o MySQL, o PostgreSQL e
o SQLite então uma pequena sobrecarga valerá a pena em função da clareza no código.

Algumas camadas de abstração foram construídas usando o padrão de namespaces PSR-0, por isso podem ser instaladas em
qualquer aplicação que você quiser:

* [Aura SQL][6]
* [Doctrine2 DBAL][2]
* [ZF2 Db][4]
* [ZF1 Db][3]

[1]: http://www.php.net/manual/pt_BR/book.pdo.php
[2]: http://www.doctrine-project.org/projects/dbal.html
[3]: http://framework.zend.com/manual/en/zend.db.html
[4]: http://packages.zendframework.com/docs/latest/manual/en/index.html#zend-db
[5]: http://php.net/manual/pt_BR/pdo.connections.php
[6]: https://github.com/auraphp/Aura.Sql

[mysql]: http://uk.php.net/mysql
[mysqli]: http://uk.php.net/mysqli
[pgsql]: http://uk.php.net/pgsql
