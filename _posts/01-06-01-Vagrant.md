---
title: Vagrant
isChild: true
anchor: vagrant
---

## Vagrant {#vagrant_title}

Rodar sua aplicação em ambientes diferentes entre desenvolvimento e produção pode levar a estranhos bugs quando
a aplicação estiver no ar. Também é complicado manter diferentes ambientes de desenvolvimento atualizados com as
mesmas versões de bibliotecas enquanto estiver trabalhando em uma equipe de desenvolvedores.

Se você estiver desenvolvendo em Windows e publicando em Linux (ou qualquer coisa que não seja Windows) ou se está
desenvolvendo em uma equipe, você deveria considerar o uso de uma máquina virtual. Pode parecer complicado, mas
usando o [Vagrant][vagrant] você poderá configurar uma máquina virtual simples com apenas alguns passos. As máquinas
virtuais base (box) podem ser configuradas manualmente, ou você pode usar um software de "provisionamento" como o
[Puppet][puppet] ou o [Chef][chef] para fazer isso por você. Provisionar o box é uma ótima maneira de garantir que
as múltiplas máquinas virtuais sejam configuradas de forma idêntica e que você não necessite manter complicadas
listas de comandos de configuração. Você pode também destruir (destroy) o box base e recriá-lo sem muitos passos
manuais, tornando fácil criar instalações novas.

O Vagrant cria pastas compartilhadas para compartilhar seu código entre sua máquina e a máquina virtual, assim você
pode criar e editar seus arquivos na sua máquina e então executar seu código dentro da máquina virtual.

### Uma pequena ajuda

Se você precisa de uma pequena ajuda para inciar o uso do Vagrant existem alguns serviços que podem ser úteis:

- [Rove][rove]: serviço que permite que você gere configurações típicas do Vagrant, sendo o PHP uma das opções. O
  provisionamento é realizado com Chef.
- [Puphpet][puphpet]: interface gráfica simples para configurar máquinas virtuais para o desenvolvimento com PHP.
  **Altamente focado em PHP**. Além de máquinas virtuais locais, pode ser usado para configurar máquinas em serviços
  de cloud. O provisionamento é feito com Puppet.
- [Protobox][protobox]: é uma camada em cima do vagrant e uma interface gráfica web para configuração de máquinas virtuais para o desenvolvimento web. Um único documento YAML controla tudo o que está instalado na máquina virtual.
- [Phansible][phansible]: oferece uma interface que ajuda a gerar regras Ansible para projetos baseados em PHP.

[vagrant]: http://vagrantup.com/
[puppet]: http://www.puppetlabs.com/
[chef]: http://www.opscode.com/
[rove]: http://rove.io/
[puphpet]: https://puphpet.com/
[protobox]: http://getprotobox.com/
[phansible]: http://phansible.com/