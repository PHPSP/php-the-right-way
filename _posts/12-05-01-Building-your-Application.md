---
title: Compilando e Implementando sua Aplicação
isChild: true
anchor: compilando_e_implementando_sua_aplicacao
---

## "Compilando" e Implementando sua Aplicação {#compilando_e_implementando_sua_aplicacao_title}

Se você se pegar fazendo alterações manuais no seu esquema do banco de dados ou rodando seus testes manualmente antes de
alterar seus arquivos (manualmente), pense duas vezes! A cada tarefa manual adicional necessária para implementar uma
nova versão da sua aplicação as chances de erros fatais são potencialmente maiores, Seja lidando com uma simples
atualização, um processo completo de implementação ou até mesmo uma estratégia de integração contínua, a
[Automação de Compilação](http://en.wikipedia.org/wiki/Build_automation) é sua amiga.

Entre as tarefas que talvez você deseja automatizar estão:

* Gerenciamento de Dependências
* Compilação e Compressão de Arquivos
* Execução de Testes
* Criação de Documentação
* Empacotamento
* Implementação

### Ferramentas de Automação

Ferramentas de automação podem ser descritas como uma coleção de scripts que tratam de tarefas comuns da implementação
de software. As ferramentas de automação não são parte da sua aplicação, elas agem na sua aplicação externamente.

Existem muitas ferramentas de código aberto disponíveis para ajudar você com o processo de automação, algumas são
escritas em PHP, outras não. Isso não deve impedi-lo de usá-las, se elas se ajustarem melhor ao trabalho em questão.
Aqui estão alguns exemplos:

[Phing](http://www.phing.info/) é o jeito mais fácil de começar com automação de implementação no PHP. Com Phing você
pode controlar os processos de empacotamento, implementação e testes através de um simples arquivo XML. Phing (Que é
baseado em [Apache Ant](http://ant.apache.org/)) fornece um rico conjunto de tarefas geralmente necessárias para 
instalar ou atualizar uma aplicação web e pode ser estendido com tarefas adicionais personalizadas, escritas em PHP.

[Capistrano](https://capistranorb.com/) é um sistema para *programadores intermediarios ou
avançados* que executa comando de forma estruturada e repetitiva em uma ou mais maquinas. Ele é pré-configurado para
implementar aplicações Ruby on Rails, entretanto pessoas estão **implementando com sucesso sistemas em PHP** com ele.
Ter sucesso com uso de Capistrano depende de um conhecimento de trabalho com Ruby e Rails.

[Chef](http://www.opscode.com/chef/) é mais que um framework de implementação, é um framework de integração bastante
poderoso escrito em Ruby que não consegue apenas implementar sua aplicação mas também construir seu ambiente de servidor
completo em maquinas virtuais.

Conteúdo sobre Chef para Desenvolvedores PHP:

* [Serie em 3 partes sobre implementação de uma aplicação LAMP com Chef, Vagrant, e EC2](http://www.jasongrimes.org/2012/06/managing-lamp-environments-with-chef-vagrant-and-ec2-1-of-3/)
* [Chef Cookbook sobre instalação e configuração de PHP 5.3 e do sistema de gerenciamento de pacotes PEAR](https://github.com/opscode-cookbooks/php)
* [Chef - série de video tutoriais por Opscode, os criadores do chef](https://www.youtube.com/playlist?list=PL11cZfNdwNyPnZA9D1MbVqldGuOWqbumZ)

Leitura Adicional:

* [Automatize seu projeto com Apache Ant](http://net.tutsplus.com/tutorials/other/automate-your-projects-with-apache-ant/)

### Integração Contínua

> Integração Contínua é uma prática de desenvolvimento de software onde membros de um time integram seu trabalho com
> frequência, geralmente essa integração ocorre diariamente - levando a muitas integrações de código por dia. Muitos
> times acreditam que essa abordagem leva a reduções significativas dos problemas de integração e permite que o time
> desenvolva software de forma coesa e rápida.

*-- Martin Fowler*

Existem diferentes formas de se implementar integração contínua com PHP. Recentemente o [Travis CI](https://travis-ci.org/)
tem feito um ótimo trabalho ao fazer da integração contínua uma realidade mesmo para pequenos projetos. O Travis CI é um
sistema de integração contínua na nuvem desenvolvido pela comunidade de código livre. Esta integrado com GitHub e oferece
suporte de primeira classe para muitas linguagens incluindo PHP.

Leitura Adicional:

* [Integração Contínua com Jenkins](http://jenkins-ci.org/)
* [Integração Contínua com PHPCI](http://www.phptesting.org/)
* [Integração Contínua com Teamcity](http://www.jetbrains.com/teamcity/)