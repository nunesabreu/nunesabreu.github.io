---
title: Problemas com Linux em notebook Acer com Intel RST
date: 2021-08-18 21:13:00
author: 
    name: Nunes Aguiar de Abreu
categories: [Dicas]
tags: [notebook, hardware, acer, ubuntu]
published: false
---

Alguns notebook Acer possuem a tecnologia de armazenamento *Rapid Storage Tecnology* (RST), da Intel. Essa tecnologia permite a utilização de HD´s como se fossem uma única unidade, semelhante ao RAID do Linux.

Ocorre que essa tecnologia não é suportada pelo Ubuntu. Assim, se você precisa instalar o Linux nesse equipamento, deve fazer algumas alterações no Windows e na própria BIOS da máquina.

O roteiro abaixo funcionou pra mim: 

1. Entre no Windows, abra o prompt de comando como admnistrador e execute: `bcdedit /set {current} safeboot minimal`
2. Reinicie o computador e pressione F2 para entrar na BIOS;
3. Vá na aba principal (main) e pressione Ctrl+S para aparecer a opção de HD;
4. Vá na opção *RST without RAID* e altere para *AHCI*;
5. Salve as configurações e reinicie o computador. O Windows deverá iniciar no modo de segurança;
6. No Windows, abra o prompt de comando como administrador e execute: `bcdedit /deleteValue {current} safeboot`
7. Reinicie o computador. Com isso, o windows já deve iniciar utilizando o modo AHCIe não o RDS. Agora você pode instalar o Linux normalmente.

## Dica:
-  O Ubuntu possui um roteiro mais longo para tentar resolver o problema: https://help.ubuntu.com/rst/. No entanto, o roteiro acima foi o suficiente no meu caso.

- Se você pretende instalar o Ubuntu no mesmo HD do Windows e, para isso, pretende formatá-lo, experimente apenas reduzir o tamanho do volume do HD utilizado pelo windows. Se o computador tiver poucos programas instalados, é provável que isso seja suficiente para obter espaço para o Linux.

![reduzir-volume-hd-windows](/assets/img/reduzir-volume-hd-windows.png)
