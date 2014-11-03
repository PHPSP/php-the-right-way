---
title: Register Globals
isChild: true
anchor: register_globals
---

## Register Globals {#register_globals_title}

**OBSERVAÇÃO:** A partir do PHP 5.4.0 a configuração `register_globals` foi removida e não pode mais ser utilizada.
Isto só foi incluído como um alerta para alguém no processo de atualização de uma aplicação legada.

Quando habilitada, a configuração `register_globals` torna disponível, no escopo global da sua aplicação, vários
tipos de variáveis (`$_POST`, `$_GET` and `$_REQUEST`). Isso pode facilmente levar a problemas de segurança pois sua
aplicação não pode dizer de forma efetiva de onde o dado está vindo.

Por exemplo: `$_GET['foo']` poderia ficar disponível via `$foo`, o que poderia sobrescrever variáveis que não tiverem
sido declaradas.  Se você estiver usando PHP < 5.4.0 __garanta__ que `register_globals` esteja __desligado__.

* [Register_globals no manual do PHP](http://www.php.net/manual/pt_BR/security.globals.php)
