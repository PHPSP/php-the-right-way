---
title: Instalação no Windows
isChild: true
anchor: instalacao_no_windows
---

## Instalação no Windows {#instalacao_no_windows_title}

Você pode fazer o download dos binários no site [windows.php.net/download][php-downloads]. Depois de extrair o arquivo baixado, é recomendado incluir na variável [PATH][windows-path] a pasta raiz do seu PHP (onde o arquivo php.exe está localizado). Dessa forma você pode executar o PHP de qualquer lugar.

Para aprender e desenvolver localmente, você pode utilizar o servidor web embutido do PHP 5.4+, de forma que você não
precisa se preocupar em configurá-lo. Se você prefere um "pacote completo" que inclui um servidor web e MySQL, então
ferramentas como [Web Platform Installer][wpi], [XAMPP][xampp], [EasyPHP][easyphp], [OpenServer][openserver] e [WAMP][wamp] irão ajudá-lo a montar rapidamente um ambiente de desenvolvimento em Windows. Dito isso, estas ferramentas serão um pouco diferentes das 
ferramentas em produção, portanto tenha cuidado quanto às diferenças de ambiente caso esteja trabalhando
em Windows e publicando em Linux. 

Caso você precise rodar seu ambiente de produção em Windows, então o IIS7 vai lhe dar mais estabilidade e melhor
performance. Você pode usar o [phpmanager][phpmanager] (um plugin GUI para o IIS7) para tornar a configuração e o
gerenciamento do PHP mais simples. O IIS7 vem com o FastCGI embutido e pronto para uso, você só precisa configurar o PHP 
como handler. Para suporte e mais recursos, existe uma [área dedicada no iis.net][php-iis] ao PHP.

Geralmente rodar sua aplicação em ambientes diferentes para desenvolvimento e produção podem levar a bugs estranhos enquanto estiverem rodando. Se você está desenvolvendo no Windows e irá fazer deploy no Linux (ou qualquer outro ambiente não Windows) então você deveria considerar usar uma [Máquina Virtual](/#virtualization_title).

Chris Tankersley tem uma postagem muito útil em quais ferramentas ele usa para o [Desenvolvimento PHP usando Windows][windows-tools].

[easyphp]: http://www.easyphp.org/
[phpmanager]: http://phpmanager.codeplex.com/
[openserver]: http://open-server.ru/
[wamp]: http://www.wampserver.com/en/
[php-downloads]: http://windows.php.net/download/
[php-iis]: http://php.iis.net/
[windows-path]: http://www.windows-commandline.com/set-path-command-line/
[windows-tools]: http://ctankersley.com/2016/11/13/developing-on-windows-2016/
[wpi]: https://www.microsoft.com/web/downloads/platform.aspx
[xampp]: http://www.apachefriends.org/en/xampp.html
