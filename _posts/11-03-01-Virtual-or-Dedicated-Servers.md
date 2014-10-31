---
title: Servidores Virtuais ou Dedicados
isChild: true
anchor: servidores_virtuais_ou_dedicados
---

## Servidores Virtuais ou Dedicados {#servidores_virtuais_ou_dedicados_title}

Se você estiver confortável com administração de sistemas, ou estiver interessado em aprender sobre isso, os
servidores virtuais ou dedicados te dão controle completo do ambiente de produção da sua aplicação.

### nginx e PHP-FPM

O PHP, por meio do seu Gerenciador de Processos FastCGI (FPM), funciona muito bem junto com o [nginx](http://nginx.or),
que é um servidor web leve e de alta performance. Ele usa menos memória do que o Apache e pode lidar melhor como
muitas requisições concorrentes. Ele é importante especialmente em servidores virtuais que não tem muita memória
sobrando.

* [Leia mais sobre o nginx](http://nginx.org)
* [Leia mais sobre o PHP-FPM](http://php.net/manual/pt_BR/install.fpm.php)
* [Leia mais sobre como configurar de forma segura o nginx e o PHP-FPM](https://nealpoole.com/blog/2011/04/setting-up-php-fastcgi-and-nginx-dont-trust-the-tutorials-check-your-configuration/)

### Apache e PHP

O PHP e o Apache tem um longo histórico juntos. O Apache é amplamente configurável e tem muitos
[módulos](http://httpd.apache.org/docs/2.4/mod/) disponíveis para estender suas funcionalidades. Ele é uma escolha
popular para servidores compartilhados e pela configuração fácil em frameworks PHP e aplicativos open source como, o
Wordpress. Infelizmente, o Apache utiliza mais recursos do que o nginx por padrão e não pode lidar com tantos
visitantes ao mesmo tempo.

O Apache tem várias configurações possíveis para executar o PHP. A mais comum e mais fácil para configurar é a
[prefork MPM](http://httpd.apache.org/docs/2.4/mod/prefork.html) com o mod_php5. Mesmo não sendo a mais eficiente em
memória, é a mais simples para começar a usar. Essa é provavelmente a melhor escolha se você não quiser entrar muito
profundamente nos aspectos de administração do servidor. Observe que, se você usar o mod_php5, terá que usar o
prefork MPM.

Alternativamente, se você quiser extrair mais performance e estabilidade do seu Apache então você poderia se
beneficiar do mesmo sistema FPM que o nginx e executar o [worker MPM](http://httpd.apache.org/docs/2.4/mod/worker.htm)
ou o [event MPM](http://httpd.apache.org/docs/2.4/mod/event.html) com o mod_fastcgi ou com o mod_fcgi. Essa
configuração será significativamente mais eficiente em relação a memória e muito mais rápida, mas gera mais trabalho.

* [Leia mais sobre o Apache](http://httpd.apache.org/)
* [Leia mais sobre os Multi-Processing Modules](http://httpd.apache.org/docs/2.4/mod/mpm_common.html)
* [Leia mais sobre o mod_fastcgi](http://www.fastcgi.com/mod_fastcgi/docs/mod_fastcgi.html)
* [Leia mais sobre o mod_fcgid](http://httpd.apache.org/mod_fcgid/)
