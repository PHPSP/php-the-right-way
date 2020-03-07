---
title: Instalação no Mac
isChild: true
anchor: instalacao_no_mac
---

## Instalação no Mac {#instalacao_no_mac_title}

O macOS já vem com o PHP, mas ele é normalmente um pouco atrasado em relação à última versão estável. Existem várias maneiras de instalar a última versão do PHP no macOS.

### Instalar PHP via Homebrew

[Homebrew] é um gerenciador de pacotes para o macOS que pode ajudá-lo a instalar facilmente o PHP e várias 
extensões. O repositório central do Homebrew contém "fórmulas" para PHP 5.6, 7.0, 7.1, 7.2, 7.3 e 7.4. Instale a última versão com este comando:

```
brew install php@7.4
```

Você pode alternar entre as versões do PHP do Homebrew modificando a variável `PATH`. Alternativamente você pode usar o [brew-php-switcher][brew-php-switcher] para alternar as versões PHP automaticamente.

### Instalar PHP via Macports

O projeto [MacPorts] é uma iniciativa da comunidade de código aberto para projetar um sistema fácil de usar para
compilar, instalar e atualizar softwares pela linha de comando, X11 ou Aqua no sistema 
operacional OS X.

O MacPorts suporta binários pré-compilados, portanto, você não precisa recompilar todas as dependências dos arquivos 
tar de origem, ele agiliza sua vida se você não tiver nenhum pacote instalado no seu sistema.

Neste ponto, você pode instalar `php54`, `php55`, `php56`, `php70`, `php71`, `php72`, `php73` ou `php74` usando o comando `port install`,
 como por exemplo:
 
 ```
    sudo port install php56
    sudo port install php74
 ```

E você pode utilizar o comando `select` para trocar a versão ativa do PHP:
```
    sudo port select --set php php74
```

### Instalar PHP via phpbrew

[phpbrew] é uma ferramenta para instalar e gerenciar múltiplas versões do PHP. Isso pode ser realmente útil se duas 
diferentes aplicações/projetos precisam de diferentes versões do PHP e você não está usando máquinas virtuais.

### Instalar PHP via instalador binário da Liip's

Outra opção popular é o [php-osx.liip.ch] que fornece métodos de instalação para versões PHP da 5.3
até a 7.3. Ele não substitui os binários do PHP instalados pela Apple, mas instala tudo em uma 
localização separada (/usr/local/php5).

### Compilar do código fonte

Outra opção que lhe dá o controle sobre a versão do PHP você instalar, é [compilar o código fonte][mac-compile].
Nesse caso, certifique-se de ter instalado o [Xcode][xcode-gcc-substitution] ou o substituto da Apple ["Command Line Tools for XCode"] que pode ser encontrado no _Apple's Mac Developer Center_.

### Instaladores _All-in-One_

As soluções listadas acima lidam apenas com o PHP e não fornecem coisas como [Apache][apache], [Nginx][nginx] ou um servidor SQL. As 
soluções _All-in-one_ como [MAMP][mamp-downloads] and [XAMPP][xampp] vão instalar estes outros programas para você e 
amarrá-los todos juntos, mas a facilidade de configuração vem com um contra-ponto de flexibilidade.

[Homebrew]: https://brew.sh/
[Homebrew PHP]: https://github.com/Homebrew/homebrew-php#installation
[MacPorts]: https://www.macports.org/install.php
[phpbrew]: https://github.com/phpbrew/phpbrew
[php-osx.liip.ch]: https://php-osx.liip.ch/
[mac-compile]: https://secure.php.net/install.macosx.compile
[xcode-gcc-substitution]: https://github.com/kennethreitz/osx-gcc-installer
["Command Line Tools for XCode"]: https://developer.apple.com/downloads
[apache]: https://httpd.apache.org/
[nginx]: https://www.nginx.com/
[mamp-downloads]: https://www.mamp.info/en/downloads/
[xampp]: https://www.apachefriends.org/index.html
[brew-php-switcher]: https://github.com/philcook/brew-php-switcher
