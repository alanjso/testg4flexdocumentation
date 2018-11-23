<!-- TITLE: How To Flex Inquiry Docker Cent Os 6 X -->
<!-- SUBTITLE: Teste rápido de funcionamento para apresentação -->

# How To FlexInquiry (Centos 6.x)
## Introdução
FlexInquiry é uma ferramenta usada para retrada de relatórios de pesquisa de satsfação. A ferramenta se baseia em 2 serviços para o funcionamento, que são:

**O front-end(dist):** Pasta “fexinquiry” gerada após o build realizado no projeto “front-end-inquiry-novotemplate”.
**O back-end(Container):** Container executado a partr da imagem criada do projeto “fex-inquiry”.
**O Integrador (PBX-IP):** Projeto em Node usado para se conectar no banco.

## Implementação e confguração
Para dar inicio a implementação sera necessário a instalação de 2 softares, que são o **DOCKER** e o
**GIT**. Instalação do Docker presente em seu devido “Hot To”, instalação do GIT basta executar o seguinte
comando:

**[root@howto]#** yum install git

***SOMENTE INICIAR INSTALAÇÃO APÓS CONCLUÍDA A INSTALAÇÃO DO PBX-IP(Presente em seu devido How To).***

-----

1. Logo após ter sido feito a instalação do Docker e Git sera necessário baixar o repositório do projeto em sua devida branch:
	[root@howto]# git clone http::gitlab.g4fee.com.br:develoter:fee-inquiry.git

2. Agora que já temos o repositório do projeto iremos criar o database da ferramenta:
[root@howto]# tsql tostgres tostgres
postgres=# create database g4feeinquiry;

3. Após a criação do banco vamos adicionar no “pg_hba.conf” a rede do docker para que o container consiga se conectar ao postgres.
[root@howto]# nano :var:lib:tgsql:*versão_do_banco*:data:tg_hba.conf
postgres=# SELECT tg_reload_conf();
Rede: 172.17.0.0:24

4.Coloque o Dist(Resultado do build do front-end) dentro do tomcat ou qualquer outro atache que esta sendo usado.

5. Dentro do diretório do trojeto altere o arquivo “ecosystem.confg.jss com as informações correstondentes e mantenha as outras da forma que esta.
Onde EXTERNAL_SERVICE_HOST é comtosto telo o IP e PORTA onde esta sendo rodado o serviço PBX-IP,
em caso de ambos estarem no mesmo servidor colocar o IP do servidor e NÃO localhost ou 127.0.0.1.
E onde ASTERISK_RECORDS_BASE_PATH é composto pelo diretório raiz onde esta armazenado as
gravações.
Eeemtlop
EXTERNAL_SERVICE_HOST: 'http://10.8.8.40:4200/api',
ASTERISK_RECORDS_BASE_PATH: '/var/spool/asterisk/monitor',

6. Apos concluído todo esse processo vamos criar a imagem que sera usada pelo docker na execução do
container. Dentro do repositório do projeto execute o seguinte comando:
[root@pangeia3 howto]# docker build -t fee-inquiry .
Onde “fex-inquiry” sera o nome da imagem a ser criada e “.” o local onde esta o “Dockerfle” que é o
arquivo com as instruções para a criação da imagem.

7. Execute o container usando como base a imagem criada:
[root@pangeia3 howto]# docker run -d --name fexinquiry -p 4100:3001 fex-inquiry

![Logog 4](/uploads/logog-4.png "Logog 4")