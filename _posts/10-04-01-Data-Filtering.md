---
title: Filtro de Dados
isChild: true
anchor: filtro_de_dados
---

## Filtro de Dados {#filtro_de_dados_title}

Nunca, jamais (nunca mesmo), confie em entradas externas feitas no seu código PHP. Sempre higienize (sanitize) e valide
as entradas externas antes de utilizá-las no seu código. As funcões `filter_var` e `filter_input` podem higienizar
textos e validar formatos (e.g. endereços de email).

Entradas externas podem ser qualquer coisa: dados de entrada de formulário `$_GET` ou `$_POST`, alguns valores na
superglobal `$_SERVER` e o corpo da requisição HTTP via `fopen('php://input', 'r')`. Lembre-se, entradas externas não
estão limitadas a dados de formulários enviados pelo usuário. Arquivos carregados e baixados, valores em sessões,
dados dos cookies e dados de web services de terceiros também são entradas externas.

Enquanto o dado externo puder ser armazenado, combinado ou acessado posteriormente, ele continua sendo uma entrada
externa. Todo momento que você processar, emitir, concatenar ou incluir dados no seu código, pergunte a si mesmo se
eles foram filtrados adequadamente e se são confiáveis.

Os dados podem ser _filtrados_ de maneiras diferentes baseando-se em sua finalidade. Por exemplo, quando entradas
externas não filtradas são passadas para uma saída de página HTML, elas podem executar HTML e JavaScript no seu site!
Isso é conhecido como Cross-Site Scripting (XSS) e pode ser um ataque bem perigoso. Um modo de evitar o XSS é
higienizar todas as tags HTML da entrada, removendo as tags ou escapando-as usando entidades HTML.

Outro exemplo é ao passar opções para execução na linha de comando. Isso pode ser extremamente perigoso (e geralmente
é má ideia), mas você pode usar a função embutida `escapeshellarg` para higienizar os argumentos executados.

Um último exemplo é aceitar entradas externas para determinar o carregamento de um arquivo do sistema de arquivos.
Isso pode ser explorado alterando o nome e o caminho do arquivo. Você precisa remover os "/", "../", [null bytes][6] e
outros caracteres do caminho do arquivo, dessa forma não será possível carregar arquivos ocultos, privados ou
confidenciais.

* [Aprenda sobre filtro de dados][1]
* [Aprenda sobre a `filter_var`][4]
* [Aprenda sobre a `filter_input`][5]
* [Aprenda sobre tratamento de null bytes][6]

### Higienização/Sanitization

A higienização remove (ou "escapa") caracteres ilegais ou inseguros das entradas externas.

Por exemplo, você deveria higienizar entradas externas antes de incluí-las no HTML ou de inserí-las em consultas SQL
brutas. Quando você usar parâmetros restritos com a [PDO](#databases), ela já irá higienizar as entradas para você.

Às vezes será obrigatório permitir algumas tags HTML seguras na sua entrada quando estiver incluindo-as em um página
HTML. Isso é bem difícil de fazer e muitas evitam isso utilizando outros formatos mais restritos, como o Markdown ou
o BBCode, embora bibliotecas para listas brancas/whitelistening, como a [HTML Purifier][html-purifier], existem por
essa razão.

[Veja sobre os Filtros de Higienização][2]

### Validação

A validação garante que as entradas externas são o que você espera. Por exemplo, você pode querer validar um endereço
de email, um número de telefone ou uma idade quando for processar o envio de um registro.

[Veja sobre os Filtros de Validação][3]

[1]: http://php.net/book.filter
[2]: http://php.net/filter.filters.sanitize
[3]: http://php.net/filter.filters.validate
[4]: http://php.net/function.filter-var
[5]: http://php.net/function.filter-input
[6]: http://php.net/security.filesystem.nullbytes
[html-purifier]: http://htmlpurifier.org/
