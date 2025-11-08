---
title: Dicas do Linux
date: 2019-04-03 09:39:22
author: 
    name: Nunes Aguiar de Abreu
image: 
    src: /assets/img/thumb-linux.jpg
categories: [Sistemas operacionais]
tags: [Linux, dicas]
published: false
---

Abaixo algumas dicas do Linux que podem ser úteis.

## Comandos
- Tamanho dos diretórios: ```du -sh *|sort -n```
- Listar os 10 maiores diretórios: ```du -x /<dir> | sort -n | tail -10```
- Listar arquivos modificados a partir de uma data: ```find . -type f -newermt YYYY-mm-dd```
- Copiar um hd inteiro: ```dd if=/dev/hd_origem of=/dev/hd_destino```

- Exemplo de utilização do **ifconfig**: ```ifconfig eth0 192.168.1.102 netmask 255.255.255.0 broadcast 192.168.1.255```
- Exemplo de utilização do AT para agendar comandos: 
	- **\# at 10pm today -f /dg/grava/reinicia.sh**
    	- Deve-se utilizar sempre com scripts
		- atq mostra a fila de comandos agendados

- Acesso remoto com ssh sem senha:
  - Na máquina remota, executar o comando ```ssh-keygen -t rsa```
  - O comando acima vai criar o arquivo id_rsa.pub. Adicione o conteúdo ao arquivo **/root/.ssh/authorized_keys** da máquina local.

- Verifcar estatísticas de escrita/leitura no disco: ```iotop```
- Listar processos em ordem de ocupação de memória: ```ps aux | sort -rnk 4```
- Listar processos em ordem de ocupação de cpu: ```ps aux | sort -rnk 3```
- Monitorar um processo: ```strace <pid>```
- Monitorar tráfego de rede: ```tcpflow -c -i <interface> port 8443```
- Verificar portas: ```netstat -tulpn```
- Verificar qual processo está utilizando uma porta: ```netstat -ltnp |grep <port>```
- Verificar informações de hardware: ```dmidecode```
- Verificar informações dos devices conectados: ```lspci -tv```

### Comandos para o Apache
- Habilitar ou desabilitar módulos: ```a2enmod, a2dismod```
- Habilitar ou desabilitar virtual host: ```a2ensite, a2dissite```
- Habilitar ou desabilitar arquivo de configuração: ```a2enconf, a2disconf```
- habilitar o rewriteEngine: ```sudo a2enmod rewrite && sudo service apache2 restart```

## Dicas
- A partir do SuSe 12.2 os serviços do sistema ficam em /lib/systemd/system com o nome \<nome\>.service. Os serviços do usuário devem ficar em /etc/systemd/system.
- Exemplo de configuração do **logRotate**:
```console
/home/meuapp/debug {
	compress
	compresscmd /bin/tar

	compressext tgz
	copytruncate
	dateext
	ifempty
	rotate 5
	size 100k
}
```
- Para que o "vi" apareça colorido, editar o arquivo **/etc/vimrc** e retirar o comentário da linha "sintax on".
- O parâmetro **load_average**, exibido no comando **top** indica, a grosso modo, a ocupação do processador. Exemplo: Se a máquina possui 1 processador com 2 núcleos, o load average máximo deveria ser igual a 2. Se estiver acima disso, significa que está havendo espera, que pode ser causada por memória, hd, etc.
  
### Reativar impressões na fila:
    - O spooler de impressão do Linux chama-se cups
	- O arquivo de configuração das impressoras fica em /etc/cups/printers.conf
	- Há uma linha no arquivo chamada "Status" que indica o status da impressora. Quando há algum problema, o cups muda o status para "Stopped". 
	- Para reativar, basta alterar o arquivo colocando o status para "Idle" e restartar o cups no init.d
	- Os logs podem ser vistos em /var/log/cups

### Criar um repositório no debian:
1. Criar um novo diretório para os arquivos .deb: 
	```console
	# cp -Rv /var/cache/apt/archives/*.deb <novo_diretorio>
	```console
2. Criar arquivo nulo acima do novo repositório:
	```console
	# cd <novo_diretorio>/..
	# touch <arquivo_nulo>
	```
3. Posicionar-se acima do novo repositório e gerar lista de pacotes: 
	```console
	# cd <novo_diretorio>/..
	# dpkg-scanpackages debs <novo_repositorio> <arquivo_nulo> | gzip > <novo_repositorio>/Packages.gz
	```
4. Adicionar caminho do novo repositório no arquivo /etc/apt/sources.list. Exemplo:
	```console
	deb file:/opt/repositorio /
	```