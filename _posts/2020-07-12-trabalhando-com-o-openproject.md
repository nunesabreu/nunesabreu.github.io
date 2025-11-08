---
title: Trabalhando com o OpenProject
date: 2019-04-03 09:39:22
author: 
    name: Nunes Aguiar de Abreu
image: 
    src: /assets/img/openproject.png
categories: [Ferramentas]
tags: [gerenciamento de projetos, ferramentas]
published: false
---

O [OpenProject](https://www.openproject.org) é uma solução completa para gerenciamento de projetos. Permite a utilização online (paga) ou opensource (instalação em um servidor próprio).
O OpenProject foi desenvolvido em Ruby e utiliza o banco de dados PostgreSQL, com a ferramenta <i>pgadmin</i>. Ele possui um <i>client</i> para controle pela linha de comando. 
Abaixo relaciono algumas dicas para trabalhar essa ferramenta.

### Sequência para trabalhar com o OpenProject:
- Definir os parâmetros essenciais na administração do sistema (usuários, definições de projeto, cores, etc).
- Se for utilizar scrum, entrar em "backlogs" e criar uma versão, que é equivalente a uma sprint;
- No quadro da sprint, adicionar as estórias de usuário;
- Ir nos pacotes de trabalho, acessar as estórias e criar as tarefas correspondentes.
	 
### Conceito e iniciação do projeto: 
- Coletar ideias, especificar escopo e entregas;
- Criar descrição do projeto e convidar membros;
	
### Definição do projeto e planejamento:
- Inserir informações detalhadas;
- Criar timeline;
- Criar pacotes de trabalho;
- Os projetos são compostos de pacotes de trabalho. Estes são divididos em subprojetos, fases e tarefas. As tarefas são as atividades que devem ser executadas.

### Comandos:
- Iniciar a interface web: `openproject run web`
- Verificar os logs: `sudo openproject logs -f --tail`
- Para alterar a senha de admin direto no sistema: 
    ```
    # openproject run rails console 
	    admin = User.where(admin: true).first
		admin.password = admin.password_confirmation = "[nova_senha]"
		admin.save(validate: false)
    ```

### Para criar hierarquias:
- Acessar os pacotes de trabalho;
- Clicar no ID da fase ou tarefa;
- Clicar em Relações;
- Selecionar "Adicionar ao filho existente"
    - Obs: Normalmente a hierarquia é Fase -> Tarefa
- Para criar um gráfico de acompanhamento, criar um Cronograma.
	
### Para configurar monitoramento de custos:
- Ir em administração - Orçamento - tipos de custo
	- Adicionar um tipo de custo.
	Ex: Name = Suporte ; Unit name = Unidades; Pluralized = Units
	- Atribuir uma taxa (rate) para o tipo de custo (será aplicado por unidade)
- Em administração - usuários, para configurar a taxa de hora para um usuário
	- Clicar no usuário desejado
	- Selecionar a aba "rate history"
	- Clicar em "Update" para configurar a taxa default, que será utilizada em todos os projetos.
	- Inserir, no campo "rate", o valor da hora do usuário.
- Selecionar o projeto desejado
- Entrar em "Configurações do projeto" e acessar a aba "modules"
- Habilitar os módulos "Time traking", "Cost Control" e "Cost Reports"
- Selecionar o menu "despesas" (budgets)
- Adicionar um nome para a despesa, associar um plano para "unit costs" e "labor costs"
- Criada a despesa, é possível associar os pacotes de trabalho a ela. Para isso, acessar "pacotes de trabalho"
	- Nos detalhes do pacote de trabalho, no quadro de custos, selecionar a despesa desejada.
	- Clicar em "More" e selecionar "log time". Especificar as horas que serão registradas no pacote de trabalho e também a atividade relacionada. Com isso, os custos já devem ser exibidos no pacote de trabalho.
	- Clicar novamente em "More" e acessar "Log unit costs". Especificar o tipo de custo e as unidades que deveriam ser registradas no pacote de trabalho.
- Voltar em "budgets" e clicar no nome da despesa desejada para comparar os custos planejados e gastos.
- Acessar os relatórios de custo para analisar o tempo gasto e o custo das unidades. Ex: Nas colunas, selecionar "week". Nas linhas, selecionar "Assignee" e "Status".
- O relatório pode se salvo para uso posterior. Também é possível tornar os resultados públicos para compartilhar com outros membros do projeto.

* * *
## Na AWS:
- Configuração para enviar e-mail pelo gmail: https://docs.bitnami.com/aws/apps/openproject/configuration/configure-smtp/
- Para saber o endereço para acesso público, iniciar a instância e depois clicar em "connect";
- No SSH, usar o login "bitnami";
- Para remover o banner da bitnami:
    ```
	$ sudo /opt/bitnami/apps/APPNAME/bnconfig --disable_banner 1
	$ sudo /opt/bitnami/ctlscript.sh restart apache
    ```
