---
isChild: true
---

## Instalação no Windows {#windows_setup_title}

O PHP está disponível de diversas maneiras no Windows. Você pode [baixar os binários](php-downloads) e até recentemente
você podia usar um instalador '.msi'. O instalador não é mais suportado e parou no PHP 5.3.0.

Para aprender e desenvolver localmente, você pode utilizar o servidor web embutido do PHP 5.4+, de forma que você não
precisa se preocupar em configurá-lo. Se você prefere um "pacote completo" que inclui um servidor web e MySQL, então
ferramentas como o [Web Platform Installer][wpi], o [Zend Server CE][zsce], o [XAMPP][xampp] e o [WAMP][wamp] irão
ajudá-lo a montar rapidamente um ambiente de desenvolvimento em Windows. Dito isso, estas ferramentas serão um pouco
diferentes das ferramentas em produção, portanto tenha cuidado quanto às diferenças de ambiente caso esteja trabalhando
em Windows e publicando em Linux. 

Caso você precise rodar seu ambiente de produção em Windows, então o IIS7 vai lhe dar mais estabilidade e melhor
performance. Você pode usar o [phpmanager][phpmanager] (um plugin GUI para o IIS7) para tornar a configuração e o
gerenciamento do PHP mais simples. O IIS7 vem com o FastCGI embutido e pronto para uso, você só precisa configurar o
PHP como handler. Para suporte e mais recursos, existe uma [área dedicada no iis.net][php-iis] ao PHP.

[php-downloads]: http://windows.php.net
[phpmanager]: http://phpmanager.codeplex.com/
[wpi]: http://www.microsoft.com/web/downloads/platform.aspx
[zsce]: http://www.zend.com/en/products/server-ce/
[xampp]: http://www.apachefriends.org/en/xampp.html
[wamp]: http://www.wampserver.com/
[php-iis]: http://php.iis.net/
