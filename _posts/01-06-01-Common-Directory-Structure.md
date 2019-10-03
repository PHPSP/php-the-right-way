---
title: Estrutura comum de diretórios
isChild: true
anchor: estrutura-comum-de-diretorios
---

## Estrutura comum de diretórios {#estrutura-comum-de-diretorios}

Um das questões comuns entre aqueles que começam q escrever programas para a web é: "onde coloco minahs coisas?"
Ao longo do tempo essa resposta sempre foi "onde está o DocummentRoot".
Embora essa resposta não esteja completa é um bom ponto por onde começar.

Por razão de segurança, os arquivos de configurações não devem ser acessíveisaos visitantes de um site, portanto,
scripts públicos são mantidos em um diretório público, configurações e dados privados são mantidos fora desse 
diretório.

para cada equipe, CMS ou Framework uma estrutura de diretório padrão é utilizada por cada uma dessas entidade. 
No entanto, se alguém estiver iniciando um projeto sozinho, saber qual estrutura de sistema de arquivos usar 
pode ser assustador.

[Paul M. Jones][pauljones] fez uma pesquisa fantástica sobre práticas comuns de dezenas de 
milhares de projetos no github no domínio do PHP. Ele compilou uma estrutura padrão de arquivos e diretórios, 
o [Standard PHP Package Skeleton][spps], com base nessa pesquisa. Nessa estrutura de diretórios, o 
``DocummentRoot`` deve apontar para ``public/``, os arquivos de testes de unidade devem estar no diretório 
``tests/`` e as bibliotecas de terceiros, instaladas pelo [composer][composer], pertencem ao diretório 
``vendor/``. Para outros arquivos e diretórios, respeitar o [Standard PHP Package Skeleton][spps] fará mais 
sentido para colaboradores de um projeto.


[pauljones]: https://twitter.com/pmjones
[spps]: https://github.com/php-pds/skeleton
[composer]: https://phptherightway.com/#composer_and_packagist
