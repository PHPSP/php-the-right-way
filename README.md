# PHP: Do Jeito Certo

## Sobre

Este é o repositório GitHub Pages para o projeto _PHP: Do Jeito Certo_, tradução brasileira do projeto _PHP: The Right Way_.

* Este website é um projeto Jekyll.
* Cada seção e sub-seção são arquivos Markdown em `_posts/`.
* Sub-seções possuem `isChild: true` em seu front matter.
* Navegação e estrutura de páginas são geradas automaticamente.

## Espalhe a palavra!

_PHP: Do Jeito Certo_ possui banners que você pode usar em seu site. Para mostrar seu apoio, deixe que novos desenvolvedores PHP saibam onde encontrar boas informações!

[Banners](http://www.phptherightway.com/banners.html)

## Instruções de Instalação

### Localmente

* Instale opcionalmente [Ruby](https://rvm.io/rvm/install/) com [Jekyll](https://github.com/mojombo/jekyll/) gem para visualizar

### Vagrant

* Instale [Vagrant](http://www.vagrantup.com/) e [VirtualBox](https://www.virtualbox.org/)
* Execute o comando `vagrant up` no diretório do projeto
* Quando o provisionamento terminar, execute `vagrant ssh -c 'cd /vagrant && jekyll serve'`
* E [visualize localmente](http://localhost:4000)

## Como contribuir

* Fork e edite
* Para criar o build com vagrant, execute `vagrant ssh -c 'cd /vagrant && jekyll build'`
* Para visualizar as alterações:
  * Execute `vagrant ssh -c 'cd /vagrant && jekyll serve'`
  * Acesse [visualize localmente](http://localhost:4000)
* Envie um pull request para análise

### Guia de Estilo para o Contribuidor

1. Use a ortografia do Português Brasileiro neste repositório.
2. Use quatro (4) espaços para identar o texto; não use TAB.
3. Limite o texto em 120 caracteres.
4. Os exemplos de código devem seguir a [PSR-1](http://www.php-fig.org/psr/psr-1/) ou superior.


### Traduzir ou não traduzir?

Tendo em vista que o projeto tem caráter didático, vale traduzir tudo que se entender importante.

Exemplos de coisas possíveis de se traduzir:

- comentários explicativos
- conteúdo de strings, heredocs ou nowdocs quando for julgado necessário etc.

Sempre avaliar o que vale ou não, pensando no caratér didático da tradução.

Reforçar que nunca se deve alterar o sentido dos textos, nem colocar informações complementares que não existem na versão original (exceto talvez alguma nota do tradutor)

## Onde

<http://www.phptherightway.com>

* [Inglês](http://www.phptherightway.com)
* [Catalão] (http://ca.phptherightway.com)
* [Chinês](http://wulijun.github.com/php-the-right-way)
* [Japonês] (http://ja.phptherightway.com)
* [Coreano] (http://wafe.github.io/php-the-right-way)
* [Italiano] (http://it.phptherightway.com)
* [Polonês](http://pl.phptherightway.com)
* [Português do Brasil](http://br.phptherightway.com)
* [Russo] (http://getjump.github.io/ru-php-the-right-way)
* [Espanhol] (http://es.phptherightway.com)
* [Ucraniano](http://iflista.github.com/php-the-right-way)
* [Búlgaro](http://bg.phptherightway.com)
* [Alemão] (http://rwetzlmayr.github.io/php-the-right-way)
* [Turco](http://hkulekci.github.io/php-the-right-way/)

### Traduções

Se você tem interesse em traduzir _PHP: The Right Way_, faça o fork do repo no GitHub e publique seu fork para sua
própria conta do GitHub. Nós vamos vincular sua tradução a partir do documento principal.

Para evitar fragmentação e confusão para o leitor, por favor escolha uma destas opções:

1. Vincularemos seu fork com a sua GitHub Page `[username].github.com/php-the-right-way`
2. Vincularemos seu fork com a sua GitHub Page com um subdomínio (por exemplo, "br.phptherightway.com")

Se você usa um subdomínio, coloque-o no arquivo `CNAME`, e avíse-nos para configurar o DNS para você. Se não usa um
subdomínio, apague o arquivo `CNAME` senão seu fork não vai fazer o build quando for publicado.

Quando sua tradução estiver pronta, abra uma issue no Isse Tracker para nos avisar.

## Porque?

Têm havido muita discussão ultimamente sobre como a comunidade PHP carece de informação válida e suficiente para programadores novos no PHP. Este repositório busca resolver este problema.

## Quem

Meu nome é [Josh Lockhart](http://twitter.com/codeguy). Sou o autor do [Slim Framework](http://www.slimframework.com/), e trabalho para a [New Media Campaigns](http://www.newmediacampaigns.com/).

### Colaboradores

* [Kris Jordan](http://krisjordan.com/)
* [Phil Sturgeon](http://philsturgeon.co.uk/)

## Licença

[Creative Commons Attribution-NonCommercial-ShareAlike 3.0 Unported License](http://creativecommons.org/licenses/by-nc-sa/3.0/)
