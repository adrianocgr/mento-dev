[‹ voltar ao README](../README.md)

# Manual Técnico de Instalação e Configuração do Ambiente de Desenvolvimento do sistema SIGA/Compras

## Índice
<li><a href="#pre-requisitos">1 - Pré-requisitos</a></li>
<li><a href="#objetivo">2 - Objetivo</a></li>
<li><a href="#configuracoes">3 - Configurações</a></li>
<li><a href="#principais-arquivos-install">3.1 - Principais arquivos de instalação para ambiente Linux</a></li>
<li><a href="#estrutura-organizacao-pastas">3.2 - Estrutura e organização das pastas</a></li>
<li><a href="#instalacao-maven">4 - Instalação do MAVEN</a></li>
<li><a href="#instalacao-git">5 - Instalação do Versionador de código GIT</a></li>
<li><a href="#autenticacao-git">5.1 - Configurar autenticação com GitLab</a></li>
<li><a href="#clonar-projetos">5.2 - Clonar projetos</a></li>
<li><a href="#instalacao-ide">6 - Instalação IDE IntelliJ</a></li>
<li><a href="#configuracao-intellij">6.1 - Configurações do IntelliJ</a></li>
<li><a href="#add-projeto-ide">6.1.1 - Adicionando Projetos no IntelliJ</a></li>
<li><a href="#integracao-jdk">6.1.2 - Configurando IntelliJ com JDK 1.7</a></li>
<li><a href="#conf-arquivo-settings">6.1.3 - Configurações do arquivo Settings</a></li>
<li><a href="#gerenciador-maven">6.1.4 - Configuração do gerenciador Maven</a></li>
<li><a href="#excludes">6.1.5 - Excludes</a></li>
<li><a href="#conf-jboss">7 - Configuração do Servidor JBOSS</a></li>
<li><a href="#plugins">8 - Plugins</a></li>
<li><a href="#atalhos-intellij">9 - Atalhos personalizados IntelliJ</a></li>
<li><a href="#instalacao-docker">10 - Instalação do Gerenciador Docker</a></li>
<li><a href="#container-docker-sqldocker-postgres">10.1 - Container Docker SQLServer/Postgres</a></li>
<li><a href="#comandos-docker">10.2 - Sintaxe e comandos Docker</a></li>
<li><a href="#conecta-e-restaura-sql">10.3 - Criar conexão e restaurar uma base de dados com SQL Server </a></li>
<li><a href="#restaurar-base-sql">10.3.1 - Restaurando base de dados SQL Server</li>
<li><a href="#conecta-postgre">10.3.2 - Criar conexão e restaurar uma base de dados com Postgres</a></li>
<li><a href="#configuracao-jrebel">11 - Configuração do servidor JRebel</a></li>

------------------------------

<h3 id="pre-requisitos">1 - Pré-requisitos</h3>

* Sistema Operacional Linux (Mint 2019.3 ou superior ou / Ubuntu 20.08 ou superior)
* 16GB de RAM
* Processador 4 núcleos ou superior.
* HD SSD 240 ou superior.


<h3 id="objetivo">2 - Objetivo</h3>
Este documento tem como objetivo auxiliar nas configurações necessárias para montar o ambiente de desenvolvimento SIGA Compras.


<h3 id="configuracoes">3 - Configurações</h3>
<h3 id="principais-arquivos-install">3.1 - Principais arquivos de instalação para ambiente Linux</h3>

* [IntelliJ](https://drive.google.com/file/d/1vtnd8t3tUeoJ4qxa-kZQjGBajmwidj9G/view?usp=sharing)
* [jboss](https://drive.google.com/file/d/1fBo7_hB7cWLxkJRcB7s2WRahcCdWamOr/view?usp=sharing)
* [Java 7 - jdk 1.7_80](https://drive.google.com/file/d/173W1nMD8j8TxEGJdmdyKGlCCaEx3OcbS/view?usp=sharing)
* [maven-3.6.1](https://drive.google.com/file/d/1qeWS23BMT5QJeeF_VzxTgQ-VGi5yaXmN/view?usp=sharing)
* [Arquivos DS de conexão com os principais Banco de dados](https://drive.google.com/file/d/1YQQ28kE-Gx7c7CxcMm7VYM8eLOprb8LG/view?usp=sharing) 
* [Backups das base de dados SQL Server Postgres](https://drive.google.com/drive/folders/1aUSgEhGCcB57BN3dPvAbjntaK5tGp4DL?usp=sharing)


<h3 id="estrutura-organizacao-pastas">3.2 - Estrutura e organização das pastas</h3>
Organizamos o ambiente criando a pasta WorkspaceAZ, dentro separamos a instalação em 3 sub-pastas.
<br> Ex:  /home/usuario-xpto/WorkspaceAZ

![3.2-001](https://i.ibb.co/bHDNWLf/img3-2.png)

A pasta /ConfigEmpresa deve armazenar arquivos como servidor de aplicação JBoos, o pacote JDK Java7, as pastas de configuração de repositório do Maven e maven-3.6.1
<br>![3.2-002](https://i.ibb.co/rxhY8HB/img3-2-002.png)

A pasta ProjetosAZ será para armazenar o espelhamento dos repositórios contendo os projetos Compras, Sigatr e Sigacomum, bem como gerenciar a pasta de Scripts das versões.
<br>![3.2-003](https://i.ibb.co/6nXmbJ8/img3-2-003.png)

Após o download dos arquivos contidos no item 3.1. faça a extração dos arquivos em suas respectivas pastas relacionadas.
Para clonar os repositórios siga os passos do item 3.4.2.

<h3 id="instalacao-maven">4 - Instalação do MAVEN</h3>
Abra o terminal (Ctrl+Alt+T) e digite os comandos a seguir:

 * Instalar Maven
~~~
$ sudo apt install maven
~~~
 * Verificar a versão do apache maven
~~~
$ mvn -version
~~~
---
<h3 id="instalacao-git">5 - Instalação do Versionador de código GIT</h3>

 * Instalar versionador GIT
~~~
$ sudo apt install git
~~~
 * Verificar a versão do GIT
~~~
$ git --version
~~~

<h3 id="autenticacao-git">5.1 -   Configurar autenticação com GitLab</h3>

Agora vamos configurar a nova chave SSH, para autenticação automática e inserir no gitlab.
<br>Abra o aplicativo terminal, e tenha certeza que está utilizando o usuário correto que deseja realizar a autenticação. Lembre-se de não utilizar o usuário root.

Obs: Para ter acesso ao Gitlab da [AZ](http://git.azi.com.br/Siga), será necessário estar conectado a [FortClient VPN](http://colaborador.azi.com.br/infra/tutorial-vpn-fortinet-linux/). Siga os passos do link para realizar a instalação da VPN na sua estação de trabalho.


* Configurar acesso de usuário com github/gitlab:
~~~
$ git config --global user.name "Fulano Xpto" </code>
 
$ git config --global user.email "meu.email@azi.com.br"
~~~

* Gerar chave de acesso para autenticação ao repositório.

Digite no terminal o comando, substituindo o e-mail, pelo seu e-mail registrado no perfil do github/gitlab:
~~~ 
$ ssh-keygen -t rsa -b 4096 -C “meu.email@azi.com.br”
~~~

Selecione o local onde deseja salvar a chave. Se apertar enter (sem escrever nada), ela será salva na sua pasta home, dentro da pasta: /.ssh/id_rsa.pub. 
Aperte a tecla “Enter” até que o arquivos id_rsa e id_rsa.pub sejam gerados no diretório: “ /home/usuario-xpto/.ssh ”

Será gerado então uma impressão digital do seu computador/servidor (key fingerprint).
<br>![5.1_001](https://i.ibb.co/vhSDFf6/img5-1-001.png)


Copiar a chave SSH (SSH key) para o GitLab
Para o GITLAB, você precisa acessar o arquivo id_rsa.pub, copiar todo seu interior e inserir na página de chaves.

* Digite o comando para abaixo no terminal para mostrar sua chave gerada ou poderá ir até o diretório "/home/user-xpto/.ssh" e abrir o arquivo id_rsa.pub em modo texto. <br>
O início da chave deve começar com ssh-rsa e terminar com o seu email escolhido.

~~~
$ cat  id_rsa.pub
~~~

Copie a chave e agora vá até o "http://git.azi.com.br" realize seu login (deverá ser seu usuário e senha de rede cadastrado da AZ) e procure pela opção “Preferences”
<br>![5.1_002](https://i.ibb.co/vLq4fJM/img5-1-002.png)

Depois cole a chave em “Key” e clique em Add key.
<br>![5.1_003](https://i.ibb.co/z6WrND5/img5-1-003.png)
 ** Depois de fazer a instalação do Git e configuração de autenticação é possível fazer o clone dos projetos.

<h3 id="clonar-projetos">5.2 - Clonar projetos</h3>
5.2.    Clonar projetos
Vá até a pasta  "/home/usuario-xpto/WorkspaceAZ/ProjetosAZ" e clique com botão direito abrir terminal e digite os comandos a seguir: 

- Clonando o projeto do Siga Compras
~~~
$ git clone git@git.azi.com.br:Siga/compras.git
~~~
![5.2_001](https://i.ibb.co/cCvNZtK/img5-2-001.png)

Para cada clone realizado aguarde até que seja finalizado o download 100%. É possível que na primeira execução do “git clone” seja solicitado seu usuário e senha de rede(AZ) para que permita realizar a ação.

- Clonando o projeto do módulo de Solicitação de Compras
~~~
$ git clone git@git.azi.com.br:Siga/sigatr.git
~~~

- Clonando a pasta de Scripts dos sistemas AZ
~~~
$ git clone git@git.azi.com.br:azi/dbscripts.git
~~~

- Clonando o projeto do Siga Comum, caso seja necessário.
~~~
$ git clone  git@git.azi.com.br:Siga/sigacomum.git (este para o siga Comum se necessário)
~~~


<h3 id="instalacao-ide">6. Instalação IDE IntelliJ</h3>

No Compras utilizamos o IntelliJ como ferramenta de desenvolvimento padrão devido a sua versatilidade, robustez, facilidade de adaptação e recursos favoráveis.

- Passo a passo para instalação.<br>
Dentro da pasta WorkspaceAZ faça a extração do pacote da IDE, e execute o arquivo 'idea.sh' que deve estar localizado no diretório:
"/home/usuario-xpto/WorkspaceAZ/idea-IU-193.7288.26/bin"

![6_001](https://i.ibb.co/2sbwdgM/img6-001.png)

Será apresentado uma tela para que permite que sejam importados configurações do intelliJ.
<br>![6_002](https://i.ibb.co/SnnBrXt/img6-002.png)

Na tela seguinte é apresentado mensagem questionando se deseja enviar relatórios de forma anônima do uso e configurações utilizadas.
<br>![6_003](https://i.ibb.co/f0NGzd7/img6-003.png)

Selecione o tema de sua preferência, claro ou escuro para o uso da IDE. Depois clique em "Next: Desktop Entry" <br>
<br>![6_004](https://i.ibb.co/mFYhd79/img6-004.png)

Clique em Next Laucher Script
<br>![6_005](https://i.ibb.co/xmh6gHf/img6-005.png)

Clique em "Next Default plugins."
<br>![6_006](https://i.ibb.co/kGxc4ZS/img6-006.png)

Clique em Next: Featured plugins
<br>![6_007](https://i.ibb.co/hDMhY68/img6-007.png)

E clique por fim em Start using IntelliJ IDEA
<br>![6_008](https://i.ibb.co/KFnKPwm/img6-008.png)
<br>![6_009](https://i.ibb.co/K98v8By/img6-009.png)


<h3 id="configuracao-intellij">6.1 - Configurações do IntelliJ</h3>
<h3 id="add-projeto-ide">6.1.1 - Adicionando Projetos no IntelliJ</h3>

Após fazer os clones dos repositórios, conforme item 5.2 e instalar o IntelliJ você poderá abrir os projetos.Lembre-se de selecionar a opção Open, selecionar o "pom.xml" do projeto desejado e selecionar a Menu File na opção Open as Project:
<br>![6.1.1_001](https://i.ibb.co/B37D0RL/img6-1-1-001.png)

Pode fazer o mesmo com o sigapregao(localizado dentro da pasta do compras), sigatr e sigacomum usando o botão Add Maven Projects que pode ser encontrado na aba do Maven no canto direito do IntelliJ.

<br>![6.1.1_002](https://i.ibb.co/4M9jBXV/img6-1-1-002.png)

Nas opções de configuração do maven marque a opção “Group Modules”


<h3 id="integracao-jdk">6.1.2 - Configurando IntelliJ com JDK 1.7</h3>

Nas opções File → Project Structure deixe marcado o Jdk 1.7 baixado anteriormente e o Language level 7 como na imagem abaixo: <br>
Para adicionar esta configuração é preciso extrair o arquivo baixado, Java 7 - jdk 1.7_80, na pasta:
<br> /home/usuario-xpto/WorkspaceAZ/configEmpresa
<br>![6.1.2_001](https://i.ibb.co/bNVkgVY/img6-1-2-001.png)
<br>![6.1.2_002](https://i.ibb.co/5rRCCVK/img6-1-2-002.png)


<h3 id="conf-arquivo-settings">6.1.3 - Configurações do arquivo Settings</h3>

- Configurando os ajustes para o arquivo “settings-AZ”.

Arquivo contendo as configurações de diretórios e acesso ao repositório [Nexus Repository Manager](http://registry.nexus.azi.srv.br).
* Download arquivo: 
[Settings](https://drive.google.com/file/d/1sMZyTH-h2ej8rpijj19cgRGlwEbIV83e/view?pasta)


Após o download, abra com editor de texto de sua preferência e ajuste as tags:
<br> < localRepository > que deve estar apontado o caminho:
<br> "/home/usuario-xpto/WorkspaceAZ/configEmpresa/mavenRepository/"

<br> < myJbossHome >, que deve estar apontado para o caminho:
<br> "/"home/usuario-xpto/WorkspaceAZ/configEmpresa/jboss5/"

Em seguida substitua as palavras chave “usuario-de-rede-AZ” , pelo seu usuário de rede e “senha-de-rede-AZ” por sua senha. Salve o arquivo e deixe-o disponível no diretório "/home/usuario-xpto/WorkspaceAZ/configEmpresa"


<h3 id="gerenciador-maven">6.1.4 - Configuração do gerenciador Maven</h3>

 Para configurar o **Maven**, utilize o menu File → Settings, procure por Build, Execution, Deployment >> Build Tools >> Maven.
A pasta mavenRepository deverá ser criada dentro da pasta /ConfigEmpresa/.
<br> O "**Maven home directory**" e "**User settings**" devem estar direcionado ao caminho dos arquivos baixados anteriormente como na imagem a seguir:
<br>![6.1.4_001](https://i.ibb.co/XxssFsk/img6-1-4-001.png)

Após isso, deve clicar na opção "Import Changes” que deve apresentar na tela.
<br>![6.1.4_002](https://i.ibb.co/qxRpm8d/img6-1-4-002.png)

Então é iniciado o download das dependências do maven.
<br>![6.1.4_003](https://i.ibb.co/tmC5rPJ/img6-1-4-003.png)

Obs: É necessário que esteja conectado ao VPN da AZ, para ter o acesso ao ambiente do Nexus e tenha êxito no download das dependências.


<h3 id="excludes">6.1.5 - Excludes</h3>

Realizar a exclusão de arquivos de assinatura digital.

Em File → Setting → Excludes adicionar os seguintes arquivos (ajuste para o seu caminho):
<br> "_/home/usuario-xpto/WorkspaceAZ/ProjetosAZ/sigatr/sigatr/sigatr-controle/src/main/java/br/com/azi/sigatr/presentation/mbean/AssinaturaDigitalApplet.java_"

<br>"_/home/usuario-xpto/WorkspaceAZ/ProjetosAZ/compras/sigacompras/sigacompras-assdigital/src/main/java/br/com/azi/util/autenticacaodigital/AutenticacaoDigitalApplet.java_"


<h3 id="conf-jboss">7 - Configuração do Servidor JBOSS</h3>

Ao clicar em Add Configuration perto do botão que sobe a aplicação iremos configurar o Jboss.
<br> ![7_001](https://i.ibb.co/CJktnXV/img7-001.png)

Selecione JBOSS →Local e preencha os seguintes campos:

- Uncheck After Launch;
- Adicione /sgc no final do link localhost:8080
- Preencha o campo "VM Options" com o seguinte texto:

~~~
-XX:MaxPermSize=512m  -server  -Xms512m  -Xmx1024m  -Xmn256m  -XX:SurvivorRatio=20  -XX:+UseConcMarkSweepGC  -XX:+UseParNewGC  -XX:+CMSParallelRemarkEnabled  -Xrs  -DcacheServer=localhost  -Dfile.encoding=UTF-8  -Dconsole.encoding=UTF-8
~~~

- Selecione o Jkd 1.7 no JRE;
- Jboss Server Instance e Port Binding set devem ter a opção default;
- Remover o Build no Before launch

No Before Launch vamos adicionar um bash que irá substituir alguns arquivos automaticamente.
<br> ![7_002](https://i.ibb.co/YLnp4Y1/img7-002.png)

Após adicionar deixe marcado apenas o que você for utilizar no momento. Se vou subir sql server local deixo apenas o script correspondente ligado.
<br> ![7_003](https://i.ibb.co/s3SD2Tm/img7-003.png)

Também é necessário que você substitua os caminhos em cada arquivo para os de sua máquina conforme deve estar disponível no diretório:
<br> " /home/usuario-xpto/WorkspaceAZ/configEmpresa/externalTool"
<br>![7_004](https://i.ibb.co/HYk1M7K/img7-004.png)

A configuração External tool deverá ficar do seguinte modo:
<br>![7_005](https://i.ibb.co/SQf2yKb/img7-005.png)


<h3 id="plugins">8. Plugins</h3>

Em File →Settings →Plugins instale o JRebel e o Lombok.
<br>![8_001](https://i.ibb.co/kBC1Y5Y/img8-001.png)


<h3 id="atalhos-intellij">9. Atalhos personalizados IntelliJ</h3>

Caso esteja acostumado com os atalhos do eclipse é possível configurar através do Menu: File /Settings / “keymap”:
<br> ![9_001](https://i.ibb.co/HnGTPc5/img9-001.png)


<h3 id="instalacao-docker">10. Instalação do Gerenciador Docker</h3>

- Instalar Docker
Abra um terminal e digite os comandos:
~~~
$ sudo apt install docker-compose
$ sudo apt install docker.io
~~~

- Verificar Status do Docker
~~~
$ sudo systemctl status docker
~~~

Dentro da pasta /home/usuario-xpto/WorkspaceAZ/ConfigEmpresa/  crie uma pasta “imagemDocker” para armazenar os Containers, conforme mostrado no item 3.2.

- Executar Container de teste no Docker.
~~~
$ sudo docker run hello-world
~~~

- Verificar containers existentes
~~~
$ sudo docker images
~~~

- Caso ocorra algum problema e precise refazer a instalação, esses são comandos para remover o docker.
~~~
$ sudo apt remove docker.io
$ sudo apt remove docker-compose
$ sudo apt autoremove
~~~
![10_001](https://i.ibb.co/JpMXW8s/img10-001.png)

Atualmente temos duas formas para subir o Container Docker com os respectivos SGBD(s) SQL Server e Postgres.


<h3 id="container-docker-sqldocker-postgres">10.1. Container Docker SQLServer/Postgres</h3>

As imagens são baixadas e montadas a partir de um único arquivo, docker-compose.yml, contendo os gerenciadores de banco de dados bancos de dados SQL Server e Postgres.

Baixe o arquivo e deixe-o disponível na diretório:
<br> "/home/usuario-xpto/WorkspaceAZ/ConfigEmpresa/imagemDocker"
- Download: [docker-compose.yml](https://drive.google.com/file/d/1aK8FOWH-ltF99sb5ewnKIzvoH_-axQrX/view?usp=sharing)

Abra o arquivo e faça os ajustes necessários de login e senha de usuário de conexão com o banco de dados.

Abra um terminal (Ctrl  + Alt + t ), dentro da pasta imagemDocker e execute o comando abaixo para copiar as imagens e criar os containers.
~~~
$ sudo docker-compose up
~~~
<br>![10.1_001](https://i.ibb.co/YPGT0yT/img10-1-001.png)


<h3 id="comandos-docker">10.2. Sintaxe e comandos Docker</h3>

1 - Verificar sintaxe
* Processar o arquivo de composição e verificar a sintaxe
~~~
$ sudo docker-compose build
~~~

2 - Fazer um teste para verificar se o arquivo “docker-compose.yml” está adequado.
* Processar o arquivo de composição e iniciar a aplicação.
~~~
$ sudo docker-compose up -d
~~~

3 - Desfazer a operação
* Para remover os containers, redes e volumes descritos no arquivo de composição.
~~~
$ sudo docker-compose down -v
~~~

4 - Executar comandos docker sem permissão de usuário sudo
~~~
$ sudo groupadd docker
$ sudo gpasswd -a usuario-xpto docker
$ sudo service docker restart
$ newgrp Docker
~~~

5 - Cria uma imagem docker de teste para verificar se o docker operacional.
~~~
$ docker container run hello-world
~~~

6 - Exibe todos os contêineres existentes 
~~~
$ docker container ps -a
~~~

* Exibe todos os containers em execução
~~~
$ docker container ps
~~~

Segue no link a documentação sobre docker:
<br> https://docs.docker.com/compose
<br>https://dev.to/ingresse/docker-e-docker-compose-um-guia-para-iniciantes-48k8


<h3 id="conecta-e-restaura-sql">10.3. Criar conexão e restaurar uma base de dados com SQL Server </h3>

Armazene o backup da base de dados SQL Server no diretório:
<br> "/home/usuario-xpto/WorkspaceAZ/ConfigEmpresa/imagemDocker/sqlserver/bkp"

No IntelliJ selecione a aba Database no canto direito clique em + data Source e selecione o SGBD Microsoft SQL Server.

![10.3_001](https://i.ibb.co/DQb613M/img10-3-001.png)
<br> Então realize o preenchimento dos Campos para conexão, Host, User, Password e realizae o download do driver. Logo teste a conexão e clique em OK.
<br> ![10.3_002](https://i.ibb.co/PWF0Sm0/img10-3-002.png)
<br> Então abra uma nova consulta utilizando o IntelliJ e execute o script de restauração da base de dados.
<br> ![10.3_003](https://i.ibb.co/bFv6sNW/img10-3-003.png)


<h3 id="restaurar-base-sql">10.3.1. Restaurando base de dados SQL Server</h3>
 
Deixe disponível o backup da base de dados SQL Server dentro da pasta:
<br> "./WorkspaceAZ/configEmpresa/imagemDocker/sqlserver/bkp" e  execute o seguinte script:

~~~
RESTORE FILELISTONLY FROM DISK = '/etc/sqlserver/bkp/COMPRAS_6_3.bak'

--If database already exists do not restore
IF DB_ID('COMPRAS_6_3') IS NULL
    BEGIN
        RESTORE DATABASE [COMPRAS_6_3] --FILE = N'COMPRAS_6_3'
        FROM DISK = N'/etc/sqlserver/bkp/compras_6_3.bak'
        WITH REPLACE , FILE = 1, NOUNLOAD, STATS = 10,
        MOVE N'COMPRAS_5_25' TO N'/etc/sqlserver/COMPRAS_6_3.mdf', --SEU nome lógico de arquivo de dados conforme mostrado pelo comando RESTORE FILELISTONLY
        MOVE N'COMPRAS_5_25_log' TO N'/etc/sqlserver/COMPRAS_6_3.ldf' --SEU nome lógico do arquivo de log, conforme mostrado pelo comando RESTORE FILELISTONLY
    END
~~~

Após o backup restaurado com sucesso deve apresentar a mensagem a seguir:

![10.3.1_001](https://i.ibb.co/YhCnVJ8/img10-3-1-001.png)

Então, abra a tela de configuração e teste a conexão novamente e na aba de ‘Schemas’ será possível marcar a opção “Current schema”, logo em novas consultas deve estar apto a 
selecionar o banco para novas consultas e utilizar o auto-complete no IntelliJ.

![10.3.1_002](https://i.ibb.co/DgwfnbD/img10-3-1-002.png)

* Script para realizar backup da base dados SQL Server

~~~
BACKUP DATABASE [COMPRAS_6_3] TO DISK = N'/etc/sqlserver/bkp/compras_6_3-teste.bak' WITH NOFORMAT, NOINIT, NAME = 'compras-full', SKIP, NOREWIND, NOUNLOAD, STATS = 10
~~~


<h3 id="conecta-postgre">10.3.2. Criar conexão e restaurar uma base de dados com Postgres</h3>
 
Armazene o backup da base de dados Postgres no diretório: 
/home/usuario-xpto/WorkspaceAZ/ConfigEmpresa/imagemDocker/postgres/bkp


No IntelliJ selecione a aba Database no canto direito clique em + data Source e selecione o SGBD Microsoft SQL Server.

![10.3.2_001](https://i.ibb.co/k1vmDbv/img10-3-2-001.png)


Informe usuário e senha conforme configurado no arquivo "docker-compose.yml"
Ex: User: postgres / senha: postgres

Realize o download dos drivers de conexão e teste a conexão. Ao realizar teste de conexao com a base deve uma mensageme sucesso.

![10.3.2_002](https://i.ibb.co/XFGSTGY/img10-3-2-002.png)

Abra um terminal, e execute os seguintes comandos para realizar restaurar a base de dados Postgres.

* Aplicar esses dois scripts na base antes de rodar o restore.
~~~
create database db_siga_pmcg;
create role dbsgc_pmcg;
create role suporteaz;
create user siga superuser createdb createrole;
comment on role siga is 'Usuário utilizado pelas aplicações do SIGA.';
create user suporteaz_full createdb;
~~~

- Restore database
~~~
$ sudo docker exec -i postgres psql -U postgres db_siga_pmcg < /home/usuario-xpto/WorkspaceAZ/configEmpresa/imagemDocker/postgres/bkp/DB_SIGA_PMCG.sql
~~~

Aguarde terminar a restauração do backup, então abra a tela de configuração e teste a conexão novamente e na aba de ‘Schemas’ será possível marcar a opção “Current schema”, logo em novas consultas deve estar apto a selecionar o banco para novas consultas e utilizar o auto-complete no IntelliJ.

![10.3.2_003](https://i.ibb.co/vdwNnvc/img10-3-2-003.png)

O arquivo docker-compose.yml contido neste documento está com a imagem do PgAdmin4, portanto é possível realizar o banco de dados Postgres através da URL:
<br> http://localhost:5050
<br> usuário: postgres@gmail.com
<br> senha: postgres


<h3 id="configuracao-jrebel">11. Configuração do servidor JRebel</h3>

* [Downlod o pacote JRebel:](https://drive.google.com/file/d/1q45_Y6EEH7aEhHmMij4oIigNEAKInIZa/view?usp=sharing)


Após o download faça a extração do pacote JrebelLicenseServerforJava dentro da pasta:
<br> /home/usuario-xpto/WorkspaceAZ/configEmpresa
<br> Abra um Terminal dentro da pastas JrebelLicenseServerforJava e execute os seguintes comandos:
~~~
$ sudo mvn package
~~~

~~~
$ sudo docker build -t jrebel-ls .
~~~

~~~
$ sudo docker run -d --name jrebel-ls --restart always -e PORT=9001 -p 9001:9001 jrebel-ls
~~~

**Você deve reiniciar o intelliJ.** e deve apresentar a mensagem solicitando a ativação do JRebel.
<br> ![11_001](https://i.ibb.co/0MrJsBs/img11-001.png)

Clique sobre o link  **“JRebel Activation”**
<br> Na tela seguinte deve ser preenchido a URL Team e seu e-mail

Acesse o endereço **http://localhost:9001**

![11_002](https://i.ibb.co/125HL1X/img11-002.png)

Então copie toda a url em vermelho {eng: } e cole na linha para ativação seguido do seu e-mail. Após o preenchimento clique para ativar a licença.

![11_003](https://i.ibb.co/n8vGd6X/img11-003.png)

<br>
<br>

---

© Copyright 2021 - All rights reserved | Todos os direitos Reservados

__AZ Tecnologia em Gestão__