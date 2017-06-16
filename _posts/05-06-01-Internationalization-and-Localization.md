---
title:   Internacionalização e Localização
isChild: true
anchor:  i18n_l10n
---

## Internacionalização (i18n) e Localização (l10n) {#i18n_l10n_title}

_Aviso para os recém-chegados: i18n e l10n são numeronyms, palavra inglesa que define um tipo de abreviação em que usa-se números 
para abreviar palavras, no nosso caso, internacionalização se torna i18n e localização, l10n._

Primeiro, precisamos definir esses dois conceitos similares e outros relacionados:


- **Internacionalização** é quando você organiza seu código de tal forma que ele possa ser adaptado para diferentes línguas e regiões
sem refatorações. Isso normalmente é feito apenas uma vez - preferencialmente, no começo do projeto, se não você provavelmente irá
precisar realizar grandes mudanças no código-fonte!
- **Localização** ocorre quando você adapta a interface (principalmente) traduzindo seu conteúdo, baseado no trabalho i18n feito
anteriormente. É normalmente realizada toda vez que uma nova língua ou região precisa de suporte e é atualizado quando algo novo é
adicionado na interface, já que ela precisará estar disponível em todas as linguagens suportadas.
- **Pluralização** define as regras necessárias entre as diferentes linguagens para que haja interoperabilidade de textos contendo
números e contadores. Por exemplo, no Inglês quando você possui apenas um item, é singular, e qualquer coisa diferente disto é 
chamado de plural; plural nessa língua é indicado pela adição de um S após algumas palavras, e algumas vezes a modificação destas.
Em outras línguas, como Russo ou Sérvio, existem duas formas de plural além da forma singular - você pode até encontrar línguas
com um total de quatro, cinco ou seis formas de pluralização, como a língua Eslovena, Irlandesa ou a Arábica.

## Formas comuns de implementar
A forma mais fácil de internacionalizar um sistema PHP é fazendo uso de arquivos de arrays de strings e utilizando essas strings em 
templates, como por exemplo `<h1><?=$TRANS['title_about_page']?></h1>`. Entretanto, essa forma não é recomendada para uso em um projeto
sério, já que apresenta diversos problemas de manutenibilidade - alguns podendo aparecer logo no começo, como a pluralização. Então,
por favor, não tente fazer isso em seu projeto caso este irá conter mais do que algumas poucas páginas.

A forma mais clássica e normalmente usada como referência a respeito de i18n e l10n é a [ferramenta Unix `gettext`][gettext].
Que data de meados de 1995 e ainda é uma completa implementação para tradução de software. É facilmente colocada em funcionamento,
e fornece poderosas ferramentas de suporte. É sobre o Gettext que iremos falar aqui. Além disso, para ajudar você a não se atrapalhar
na linha de comando, estaremos apresentando uma incrível aplicação gráfica que pode ser usada para facilmente atualizar seus arquivos
fontes l10n.

### Outras ferramentas

Existem algumas bibliotecas comumentemente utilizadas para suportar o Gettext e outras implementações do i18n. Algumas
podem possuir uma instalação mais fácil ou fornecer funções ou formatos de arquivos i18n adicionais. Nesse documento,
iremos focar nas ferramentas fornecidas nativamente pelo PHP. Abaixo listamos outras opções de bibliotecas:

- [oscarotero/Gettext][oscarotero]: suporte a Gettext com uma interface OO; inclui funções auxiliares melhoradas, poderosos
extratores para diversos formatos de arquivos (alguns desses não suportados nativamente pelo comando `gettext`), e também pode
exportar para outros formatos de arquivos além de `.mo/.po`. Pode ser útil se você precisa integrar seus arquivos de tradução
em outras partes do sistema, como em uma interface JavaScript.
- [symfony/translation][symfony]: suporte a diversos formatos de arquivos, mas recomenda o uso do formato XLIFF. Não inclui
funções auxiliares e nem um extrator incorporado, mas suporta placeholders usando `strtr()` internamente.
- [zend/i18n][zend]: suporte a arrays e arquivos INI, ou formatos Gettext. Implementa uma camada de cache para evitar que 
sejam feitas leituras do sistema de arquivos a todo momento. Inclui também auxiliadores de interface, filtros de entrada 
locale-aware e validadores. Entretanto, não possui nenhum extrator de mensagens.

Outros frameworks também incluem módulos i18n, mas estes não estão disponíveis fora de sua base de código:
- [Laravel] suporte a arquivos de array básicos, não possui um extrator automático mas inclui um helper `@lang` para os 
arquivos de template.
- [Yii] suporta array, Gettext, e tradução orientada a base de dados, além de incluir um extrator de mensagens. É endorsado
pela extensão [`Intl`][intl], disponível desde o PHP 5.3, e baseado no [ICU project]; faz com que seja possível o Yii executar
poderosas substituições, como soletração de números, formatação de datas, horários, intervalos, unidades monetárias, e ordinais.

Se você decidir fazer uso de alguma das bibliotecas que não fornece extratores, você pode utilizar os formatos Gettext, de forma
que seja possível utilizar o conjunto de ferramentas originais do Gettext (incluindo o Poedit) que serão descritas neste capítulo.

## Gettext

### Instalação
Você pode precisar instalar o Gettext e outras bibliotecas PHP relacionadas utilizando seu gerenciador de pacotes,
como `apt-get` ou `yum`.
Após instalado, habilite adicionando `extension=gettext.so` (Linux/Unix) ou `extension=php_gettext.dll` (Windows) ao
seu `php.ini`.

Nós também iremos fazer uso do [Poedit] para criar os arquivos de tradução. Você provavelmente irá acha-lo no gerenciador de
pacotes de seu sistema; está disponível para Unix, Mac, e Windows, e também pode ser [baixado gratuitamente em seu website][poedit_download].

### Estrutura

#### Tipos de arquivos
Existem três arquivos que você normalmente terá de lidar enquanto trabalha com o Gettext. Os principais são os arquivos
PO (Portable Object) e MO (Machine Object), sendo o primeiro a lista legível dos "objetos traduzidos" e o segundo, o
binário correspondente que será utilizado pelo interpretador Gettext quando este estiver realizando a localização. 
Além destes dois, temos também o arquivo POT (Template), que contém basicamente todas as chaves existentes de seus
arquivos-fonte, e que é utilizado para auxiliar na geração e atualização dos arquivos PO. Esses arquivos template
não são mandatórios: dependendo da ferramenta que você estiver utilizando para realizar l10n, você pode utilizar apenas
arquivos PO/MO sem maiores problemas.
Sempre irá existir um par de arquivos PO/MO por língua e região, mas apenas um arquivo POT por domínio.

### Domínios
Existem algumas situações, em grandes projetos, nas quais você pode vir a necessitar de traduções diferentes para a 
mesma palavra, quando estas possuírem diferentes significados conforme o contexto. Nesses casos, você tera de
separa-las em diferentes _domínios_. Que são basicamente nomes para grupos de arquivos POT/PO/MO, aonde o nome desse
arquivo é o _domínio de tradução_. Pequenos e médios projetos, normalmente visando uma menor complexidade, utilizam
apenas um domínio; seu nome é arbitrário, mas estaremos usando "main" para nossos códigos de exemplo.
Em projetos [Symfony], por exemplo, domínios são utilizados para separar a tradução das mensagens de validação.

#### Código de local (Locale code)
Um local é um código simples para identificar uma versão de uma língua. É definido seguindo as especificações [ISO 639-1][639-1]
e [ISO 3166-1][3166-1]: duas letras minúsculas que representam a língua, opcionalmente seguidas por um underline
e duas letras maiúsculas identificando o país ou código regional. Para [línguas raras][rare], são utilizadas três letras.

Para alguns falantes, a parte do país pode parecer redundante. Entretanto, algumas línguas possuem dialetos
em países diferentes, como por exemplo o Alemão Austríaco (`de_AT`) ou o Português Brasileiro (`pt_BR`). A
segunda parte é utilizada para distinguir esses dialetos - quando não for presente, é tomada como uma versão
"genérica" ou "híbrida" da língua.

### Estrutura de diretórios
Para fazer uso do Gettext, iremos precisar aderir a uma estrutura específica de pastas. Primeiro, você irá precisar
selecionar uma raiz arbitrária para seus arquivos l10n na raiz de seu repositório. Dentro dela, você terá uma pasta
para cada um dos locais necessários, e uma pasta fixa `LC_MESSAGES` que deve conter todos os pares de arquivos PO/MO.
Exemplo:

{% highlight console %}
<raiz do projeto>
 ├─ src/
 ├─ templates/
 └─ locales/
    ├─ forum.pot
    ├─ site.pot
    ├─ de/
    │  └─ LC_MESSAGES/
    │     ├─ forum.mo
    │     ├─ forum.po
    │     ├─ site.mo
    │     └─ site.po
    ├─ es_ES/
    │  └─ LC_MESSAGES/
    │     └─ ...
    ├─ fr/
    │  └─ ...
    ├─ pt_BR/
    │  └─ ...
    └─ pt_PT/
       └─ ...
{% endhighlight %}

### Formas de pluralização
Assim como dito na introdução, diferentes línguas podem apresentar diferentes regras de pluralização. Entretanto, o 
Gettext nos salva deste problema mais uma vez. Quando estiver criando um novo arquivo `.po`, você precisará declarar as
[regras de pluralização][plural] para aquela língua, e os pedaços traduzidos que são sensíveis à pluralização irão ter
uma forma diferente para cada uma dessas regras. Quando estiver chamando o Gettext no código, você terá de especificar
o número relacionado a sentença, para que assim possa ser feita o uso correto da língua - até mesmo utilizando 
substituição de texto quando necessário.

Regras de pluralização incluem o número de plurais disponíveis e um teste booleano com `n` que irá definir em qual
regra dado número cai (começando a conta com 0). Por exemplo:

- Japonês: `nplurals=1; plural=0` - apenas uma regra
- Inglês: `nplurals=2; plural=(n != 1);` - duas regras, primeira se N for um, segunda regra nos outros casos
- Português Brasileiro: `nplurals=2; plural=(n > 1);` - duas regras, segunda se N for maior do que um, primeira
nos outros casos

Agora que você entende a base de como as regras de pluralização funcionam - e se caso não tenha, por favor olhe
uma explicação mais profunda no seguinte [tutorial LingoHub][lingohub_plurals] -, você talvez queira copiar os
necessários de uma [lista][plural] ao invés de escrevê-los do zero.

Quando estiver chamando o Gettext para fazer localização em sentenças com contadores, você deverá dar a ele o
número relacionado. O Gettext irá decidir qual regra deve ser utilizada e irá usar a versão correta da localização.
Você precisará incluir no arquivo `.po` uma sentença diferente para cada regra de pluralização definida.

### Exemplo de Implementação
Após toda essa teoria, vamos ser um pouco mais práticos. Aqui está um fragmento de um arquivo `.po` - não se preocupe
com seu formato, mas com seu conteúdo como um todo, você irá aprender mais tarde a como facilmente modifica-los:

{% highlight po %}
msgid ""
msgstr ""
"Language: pt_BR\n"
"Content-Type: text/plain; charset=UTF-8\n"
"Plural-Forms: nplurals=2; plural=(n > 1);\n"

msgid "We're now translating some strings"
msgstr "Agora nós estamos traduzindo algumas strings"

msgid "Hello %1$s! Your last visit was on %2$s"
msgstr "Olá %1$s! Sua última visita foi em %2$s"

msgid "Only one unread message"
msgid_plural "%d unread messages"
msgstr[0] "Só uma mensagem não lida"
msgstr[1] "%d mensagens não lidas"
{% endhighlight %}

A primeira seção funciona como o cabeçalho, possuindo o `msgid` e `msgstr` especialmente vazios. Descreve a codificação
do arquivo, formas de pluralização e outros detalhes menos relevantes.
A segunda seção traduz um texto simples do Inglês para o Português Brasileiro, e a terceira faz o mesmo, mas alavancando
substituição de texto em [`sprintf`][sprintf] para que a tradução contenha o nome do usuário e a data de visita.
A última seção é um fragmento de formas de pluralização, mostrando a forma singular e plural sendo `msgid` em Inglês e sua
tradução correspondente em `msgstr` 0 e 1 (seguindo o número dado pela regra de pluralização). Então, substituição de texto
é utilizada para que o número possa ser representado diretamente na sentença, utilizando `%d`. A forma plural sempre terá
dois `msgid` (singular e plural), então é recomendando que não seja utilizada uma língua complexa como fonte para tradução.

### Discussão acerca das chaves l10n
Como você deve ter notado, nós estamos usando como ID as sentenças em Inglês. Esse `msgid` é o mesmo a ser usado em
todos seus arquivos `.po`, ou seja, outras línguas irão ter o mesmo formato e o mesmo campo de `msgid` com suas
traduções nas linhas `msgstr` correspondentes.

A respeito das chaves de traduções, temos duas principais "linhas de pensamento":

1. _`msgid` sendo uma sentença real_.  
    As principais vantagens são: 
    - Se existem pedaços do software não traduzidos em qualquer língua, a chave exibida na interface ainda irá manter
    um significado. Exemplo: se você puder traduzir do Inglês para o Espanhol sem dificuldades, mas precisar de ajuda
    para traduzir para o Francês, você pode publicar a nova página com as sentenças em Francês faltantes, essas partes
    irão então exibir as sentenças em Inglês no lugar das faltantes;
    - É muito mais fácil para o tradutor entender o que está acontecendo e fazer uma tradução adequada baseando-se
    apenas no `msgid`;
    - Te da "gratuitamente" l10n de uma língua - a língua-mãe do sistema;
    - A unica desvantagem: se você precisar mudar o texto, você precisará substituir o `msgid` correspondente em todos
    os arquivos das línguas.

2. _`msgid` sendo uma chave única estruturada_.  
Pode descrever o papel da sentença na aplicação de forma estrutura, incluindo o template ou parte aonde o texto está
localizado ao invés de seu conteúdo.
    - é uma ótima forma de ter seu código organizado, separando o conteúdo do texto da lógica do template.
    - entretanto, isso pode vir a trazer problemas para o tradutor pois ele pode vir a perder o contexto. Além disso,
    um arquivo de língua principal seria necessário como base para as outras traduções. Exemplo: o desenvolvedor deveria
    ter um arquivo `en.po`, o qual tem de ser lido pelos tradutores para entender o que escrever num arquivo `fr.po`.
    - traduções faltantes mostrariam chaves sem sentido na tela (`top_menu.welcome` ao invés de `Hello there, User!`
    numa página não traduzida em Francês por exemplo). Isso é bom no sentido de forçar a tradução antes da publicação -
    mas ruim pois problemas de tradução causariam falhas terriveis de interface. Algumas bibliotecas incluem a opção
    de especificar uma língua como "fallback", para que seja possível ter um comportamento parecido com o da primeira
    abordagem e evitar esse problema.

O [manual do Gettext][manual] favorece a primeira abordagem, já que num geral, é mais fácil para os tradutores e usuários
no caso de ocorrer algum problema. Será essa a abordagem utilizada aqui também. Entretanto, a [documentação do Symfony][symfony-keys] favorece a segunda abordagem, visando permitir mudanças independente de todas as traduções sem que afete também os templates.

### Uso no dia-a-dia
Em uma aplicação comum, você irá usar algumas funções do Gettext enquanto escreve textos estáticos nas suas páginas. Essas
sentenças irão aparecer então nos arquivos `.po`, serem traduzidas, compiladas em arquivos `.mo` e então, usadas pelo Gettext
quando estiver sendo feita a renderização da interface. Dado isso, vamos interligar tudo que discutimos até agora em
um exemplo passo a passo:

#### 1. Exemplo de um arquivo template, incluindo algumas chamadas gettext diferentes
{% highlight php %}
<?php include 'i18n_setup.php' ?>
<div id="header">
    <h1><?=sprintf(gettext('Welcome, %s!'), $name)?></h1>
    <!-- código indentado dessa forma apenas visando legibilidade -->
    <?php if ($unread): ?>
        <h2><?=sprintf(
            ngettext('Only one unread message',
                     '%d unread messages',
                     $unread),
            $unread)?>
        </h2>
    <?php endif ?>
</div>

<h1><?=gettext('Introduction')?></h1>
<p><?=gettext('We\'re now translating some strings')?></p>
{% endhighlight %}

- [`gettext()`][func] traduz uma `msgid` para sua correspondente `msgstr` numa língua especifica. Existe também a função
abreviada `_()` que serve o mesmo propósito;
- [`ngettext()`][n_func] faz o mesmo mas com regras de pluralização;
- existem também as funções [`dgettext()`][d_func] e [`dngettext()`][dn_func], que permitem sobrescrever o domínio em uma
chamada específica. Será mostrado mais sobre configuração de domínios no próximo exemplo.

#### 2. Um exemplo de arquivo de configuração (`i18n_setup.php` conforme acima), selecionando o local correto e configurando o Gettext
{% highlight php %}
<?php
/**
 * Verifica se um $locale informado é suportado no projeto
 * @param string $locale
 * @return bool
 */
function valid($locale) {
   return in_array($locale, ['en_US', 'en', 'pt_BR', 'pt', 'es_ES', 'es']);
}

// Definindo o locale padrão, por motivos informacionais
$lang = 'en_US';

if (isset($_GET['lang']) && valid($_GET['lang'])) {
    // o locale pode ser mudado através da query-string
    $lang = $_GET['lang'];    // você deve sanitizar essa parte!
    setcookie('lang', $lang); // está armazenado em um cookie então pode ser reusado
} elseif (isset($_COOKIE['lang']) && valid($_COOKIE['lang'])) {
    // se um cookie com essa informação existe, utilizamos ele
    $lang = $_COOKIE['lang']; // você deve sanitizar essa parte!
} elseif (isset($_SERVER['HTTP_ACCEPT_LANGUAGE'])) {
    // padrão: olhe para as outras línguas que o navegador diz serem aceitas pelo usuário
    $langs = explode(',', $_SERVER['HTTP_ACCEPT_LANGUAGE']);
    array_walk($langs, function (&$lang) { $lang = strtr(strtok($lang, ';'), ['-' => '_']); });
    foreach ($langs as $browser_lang) {
        if (valid($browser_lang)) {
            $lang = $browser_lang;
            break;
        }
    }
}

// aqui definimos a variável de ambiente locale para o sistema conforme o que foi definido acima
putenv("LANG=$lang");

// pode ser útil para funções que envolvam dastas (LC_TIME) ou formatações de valores monetários (LC_MONETARY)
setlocale(LC_ALL, $lang);

// faz com que o Gettext procure por ../locales/<lang>/LC_MESSAGES/main.mo
bindtextdomain('main', '../locales');

// determina em qual codificação o arquivo deve ser lido
bind_textdomain_codeset('main', 'UTF-8');

// se a sua aplicação possui domínios adicionais, como citado anteriormente, você deve vincula-los aqui
bindtextdomain('forum', '../locales');
bind_textdomain_codeset('forum', 'UTF-8');

// aqui indicamos qual será o domínio padrão no qual chamadas gettext() irão responder
textdomain('main');

// isso procuraria pela string em forum.mo ao invés de main.mo
// echo dgettext('forum', 'Welcome back!');
?>
{% endhighlight %}

#### 3. Preparando uma tradução pela primeira vez
Visando simplificar as coisas - e uma das principais vantagens que o Gettext possui em relação a outros frameworks i18n -
é seu tipo de arquivo customizável. "Nossa, isso é muito difícil de entender e alterar, um simples array seria muito mais
fácil!". Não cometa erros, aplicações como a [Poedit] estão aqui para ajudar - _bastante_. Você pode obtê-la através de
[seu website][poedit_download], é gratuita e está disponível para todas as plataformas. É uma ferramenta muito fácil de
utilizar, e ao mesmo tempo muito poderosa - utilizando todos os poderosos recursos que o Gettext fornece.

No primeiro uso, você deve selecionar "File > New Catalog" no menu. Lá, você irá ter uma pequena janela aonde iremos preparar
o terreno para tudo fluir naturalmente. Você poderá encontrar essas configurações mais tarde em "Catalog > Properties":

- Project name and version, Translation Team and email address (Nome do projeto e versão, Time de Tradução e endereço de 
e-mail): Informação útil que vai no cabeçalho do arquivo `.po`;
- Language (Língua): aqui você deve utilizar o formato mencionado anteriormente, como por exemplo `en_US` ou `pt_BR`;
- Charsets (Codificação dos caracteres): UTF-8, preferencialmente;
- Source charset (Codificação dos caracteres dos seus arquivos-fonte): coloque aqui a codificação utilizada pelos seus
arquivos PHP - provavelmente UTF-8, certo?
- plural forms (Formas de pluralização): aqui vão as regras mencionadas anteriormente - há um link aqui com exemplos;
- Source paths (Caminhos fonte): aqui devem ser incluídos todas as pastas do seu projeto aonde `gettext()` (e similares)
serão utilizados - normalmente a pasta(s) que possui os templates da sua interface
- Source keywords (Fonte das palavras-chave): essa última parte é preenchida por padrão, mas talvez você queira altera-la
mais tarde - e isso é um dos pontos mais poderosos do Gettext. O software subjacente sabe como que a chamada `gettext()`
se apresenta nas mais diversas linguagens de programação, mas você talvez queira criar suas próprias formas de tradução. 
Isso será discutido mais a frente na seção "Dicas".

Após configurar esses pontos, será pedido que você salve o arquivo - utilizando a estrutura de diretórios que mencionamos,
e então irá realizar um mapeamento nos seus arquivos-fonte para encontrar as chamadas de localização. Essas serão postas
vazias na aba de tradução, e você deve começar a escrever as versões localizadas dessas mensagens. Salve e um arquivo `.mo` 
irá ser (re)compilado na mesma pasta. E é isso, seu projeto agora está internacionalizado.

#### 4. Traduzindo mensagens
Como você deve ter notado, existem dois tipos principais de mensagens: as simples e aquelas com formas plurais. As primeiras
possuem apenas duas caixas: a fonte e a mensagem localizada. A mensagem fonte não pode ser modificada tanto que o 
Gettext/Poedit não incluem os poderes de você alterar os arquivos-fonte - você deve muda-los separadamente e escaneá-los.
Dica: você pode clicar com o botão direito do mouse em uma linha de tradução para descobrir quais os arquivos-fonte e linhas
no qual essa mensagem está sendo usada.
Por outro lado, formas plurais das mensagens incluem duas caixas mostrando as duas mensagens, e abas para que você
consiga configurar as diferentes formas finais.

Sempre que você mudar seus arquivos-fonte e precisar atualizar as traduções, apenas aperte Refresh (Atualizar) para que
o Poedit escaneie seu código, removendo as entradas que não existem mais, mesclando as que mudaram e adicionando as novas.
Também pode vir a tentar adivinhas algumas das traduções, baseando-se em outras que você tenha feito. Essas tentativas de
adivinhação e as mudanças irão receber um marcador de indefinição, identificando que há a necessidade de revisão, sendo
destacadas na lista. É útil também caso você tenha um time de tradução e alguém tente escrever algo que eles não tenham certeza
a respeito: apenas coloque o marcador de indefinição e alguém irá revisar essa parte mais tarde.

Finalmente, é recomendado que você deixe marcada a opção "View > Untranslated entries first", já que essa irá te ajudar 
_muito_ a não esquecer as entradas ainda não traduzidas. Através desse menu, você pode abrir partes da Interface
Gráfica que permitem deixar informações a respeito do contexto para ajudar os tradutores, se necessário.

### Dicas e Truques

#### Possíveis problemas de cacheamento
Se você estiver rodando o PHP como um módulo no Apache (`mod_php`), você pode vir a enfrentar problemas com o arquivo
`.mo` sendo cacheado. Isso ocorre na primeira vez que este é lido, e então, para conseguir atualizar você pode vir
a precisar reiniciar o servidor. No Nginx e PHP5 normalmente leva apenas algumas atualizações na página para que o 
cache seja atualizado, e no PHP7 isso é raramente necessário.

#### Funções auxiliares adicionais
Conforme preferência de muitas pessoas, é mais fácil utilizar `_()` no lugar de `gettext()`. Muitas bibliotecas i18n
customizadas de outros frameworks utilizam também algo similar a `t()`, visando manter o código traduzível menor.
Entretanto, essa é a única função que fornece um atalho. Você talvez queira adicionar algumas outras no seu projeto,
como `__()` ou `_n()` para `ngettext()`, ou um extravagante `_r()` que se juntaria as chamadas `gettext()` e `sprintf()`.
Outras bibliotecas, como a [oscarotero's Gettext][oscarotero] também fornecem funções auxiliares parecidas com essas.

Nesses casos, você precisará instruir a ferramenta Gettext a como extrair as mensagens dessas novas funções. Não tenha
medo, é bem fácil. É apenas um campo no arquivo `.po` ou uma Configuração na janela do Poedit. No editor, essa opção
encontra-se no caminho "Catalog > Properties > Source keywords". Você precisa incluir lá as especificações dessas novas
funções, seguindo um [formato específico][func_format]:

- se você criar algo parecido com `t()` que simplesmente retorne a tradução para uma mensagem, você pode especificar
isso como `t`. O Gettext vai saber que o único argumento é a mensagem a ser traduzida;
- se a função possui mais do que um argumento, você pode especificar em qual deles a mensagem se encontra - e se
necessário, também a forma plural. Para exemplificar, se chamarmos nossa função assim: `__('one user', '%d users', $number)`,
a especificação será `__:1,2`, significando que a primeiro forma é o primeiro argumento, e a segunda forma é o segundo
argumento. Mas se ao invés seu número vier como primeiro argumento, a especificação seria `__:2,3`, identificando que a primeira
forma é o segundo argumento, e assim por diante.

Após incluir essas novas regras no seu arquivo `.po`, um novo escaneamento irá trazer suas novas mensagens, simples assim.

### Referências

* [Wikipedia: i18n e l10n](https://pt.wikipedia.org/wiki/Internacionalização_(informática))
* [Wikipedia: Gettext](https://pt.wikipedia.org/wiki/Gettext)
* [LingoHub: Tutorial de internacionalização PHP com gettext][lingohub]
* [Manual do PHP: Gettext](http://php.net/manual/pt_BR/book.gettext.php)
* [Manual do Gettext][manual]

[Poedit]: https://poedit.net
[poedit_download]: https://poedit.net/download
[lingohub]: https://lingohub.com/blog/2013/07/php-internationalization-with-gettext-tutorial/
[lingohub_plurals]: https://lingohub.com/blog/2013/07/php-internationalization-with-gettext-tutorial/#Plurals
[plural]: http://docs.translatehouse.org/projects/localization-guide/en/latest/l10n/pluralforms.html
[gettext]: https://pt.wikipedia.org/wiki/Gettext
[manual]: http://www.gnu.org/software/gettext/manual/gettext.html
[639-1]: https://pt.wikipedia.org/wiki/ISO_639
[3166-1]: https://pt.wikipedia.org/wiki/ISO_3166-1
[rare]: http://www.gnu.org/software/gettext/manual/gettext.html#Rare-Language-Codes
[func_format]: https://www.gnu.org/software/gettext/manual/gettext.html#Language-specific-options
[oscarotero]: https://github.com/oscarotero/Gettext
[symfony]: https://symfony.com/doc/current/components/translation.html
[zend]: https://docs.zendframework.com/zend-i18n/translation
[laravel]: https://laravel.com/docs/master/localization
[yii]: http://www.yiiframework.com/doc-2.0/guide-tutorial-i18n.html
[intl]: http://php.net/manual/pt_BR/book.intl.php
[ICU project]: http://www.icu-project.org
[symfony-keys]: https://symfony.com/doc/current/components/translation/usage.html#creating-translations

[sprintf]: http://php.net/manual/pt_BR/function.sprintf.php
[func]: http://php.net/manual/pt_BR/function.gettext.php
[n_func]: http://php.net/manual/pt_BR/function.ngettext.php
[d_func]: http://php.net/manual/pt_BR/function.dgettext.php
[dn_func]: http://php.net/manual/pt_BR/function.dngettext.php