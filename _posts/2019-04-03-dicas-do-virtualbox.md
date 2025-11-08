---
title: Dicas do Virtualbox
date: 2019-04-03 09:45:13
author: 
    name: Nunes Aguiar de Abreu
tags: [virtualbox]
image: 
    src: /assets/img/thumb-virtualbox.jpg
categories: [Dicas]
tags: [virtualbox]
published: false
---

O VirtualBox é uma ótima ferramenta para o gerenciamento de máquinas virtuais.
Abaixo descrevo alguns comandos úteis para sua utilização pela linha de comando.

### Comandos para executal no shell

- Iniciar uma máquina: `VBoxManage startvm "Nome-da-VM" --type headless`
- Parar uma máquina: `VBoxManage controlvm "Nome-da-VM" acpipowerbutton`
- Listar as máquinas disponíveis: ```VBoxManage list vms```
- Restaurar ao último snapshot: ```VBoxManage snapshot "Nome-da-VM" restorecurrent```
- Desligar por ACPI (pressionar botão de desligar): ```VBoxManage controlvm "Nome-da-VM" acpipowerbutton && sleep 30```
- Desligar (tirar da tomada): ```VBoxManage controlvm "Nome-da-VM" poweroff```
- Ligar a máquina: ```/usr/bin/VBoxManage startvm "Nome-da-VM" --type headless```
- Resetar: ```VBoxManage controlvm Nome-da-VM reset```
- Instalar um pacote de extensões: ```VBoxManage extpack install <pacote_vbox-extpack>```
- Registrar uma VM: ```VBoxManage registervm <arquivo vbox>```

- Para habilitar a permissão de acesso às pastas montadas pelo virtualbox, utilize este comando: ```usermod -aG vboxsf $(whoami)```

### Interface web para gerenciamento
- Interface web para gerenciamento: https://github.com/phpvirtualbox/phpvirtualbox
- Correção para o virtualbox 6.1: https://github.com/phpvirtualbox/phpvirtualbox/issues/210
- Correção para pastas compartilhadas: https://github.com/trasherdk/phpvirtualbox/blob/d5a69690b0904e0982a536fe13f6b837ed01a48a/update-6.0.10-linux.md
- Instalação com Nginx: https://nets-nuts.com.br/como-instalar/phpvirtualbox-com-nginx/
