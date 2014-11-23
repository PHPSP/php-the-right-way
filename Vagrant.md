# Contribuir com o projeto utilizando o Vagrant

### Instalar o vagrant
* Instale [Vagrant](http://www.vagrantup.com/) e [VirtualBox](https://www.virtualbox.org/)
* Execute o comando `vagrant up` no diretório do projeto

### Gerar o build do projeto e visualizar localmente
* Realize as alterações
* Para criar o build:
  * Execute `vagrant ssh -c 'cd /vagrant && jekyll build'`
* Para visualizar as alterações:
  * Execute `vagrant ssh -c 'cd /vagrant && jekyll serve --host 10.0.2.15'`
  Onde `10.0.2.15` é o IP padrão da máquina virtual. Se posto `localhost` não funcionará.
  * Acesse [visualize localmente](http://localhost:4000)

----------
# Nota importante:

Executar `vagrant ssh -c 'jekyll build --watch'` não surtirá efeito, pois a opção `--watch`,
aparentemente, só funciona quando as alterações são feitas na máquina que executa o watch.
Ao alterar os arquivos no host, não serão recompilados os arquivos md.

Você pode, portanto, executar o comando que inicia o servidor http e, com o servidor rodando,
executar o build do projeto. A cada build, os arquivos são interpretados novamente e bastará
atualizar o navegador para visualizar as alterações.