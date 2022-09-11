## MINICURSO DE LINUX PARA DEVOPS ##

>O que devo conhecer
1. Estrutura de pastas
* Mais utilizados: var, tmp, opt, etc, bin, home

/var : Onde se encontram os arquivos dinâmicos 

/tmp : Pasta temporária, utilizado para copiar e modificar arquivos

/mnt : Ponto de montagem (HD temporário por exemplo)

/opt :  Instalação de Softwares complementares não nativos do Linux

/etc : Principal pasta do Linux (parte de configuração de sistema e software - configuração de nginx, apache, porta ssh)

/bin : Onde ficam os binários do Linux (comandos Linux) - qualquer usuário pode utilizar

/sbin :  bin com privilégios

/dev : Onde se encontram os dispositivos (HDs, pendrives)

/home : Diretório dos usuários

/root : Diretório do usuário root

/media : onde são montados os pendrives

/proc : informações de hardware da máquina

2. Comandos essenciais

pwd : mostra diretorio atual

cd : acessa um diretório

ls : lista o conteudo

mkdir : cria um diretório

touch : alterar a data de criação de um arquivo

rm : apaga arquivos

mv : mover e renomear

cp : copiar arquivos

find : procurar arquivos

clear : limpa a tela

yum/dnf/opt : instalar e remover pacotes no linux

service : gerenciar serviço

tail/cat : log de serviços

useradd : criar usuário

passwd : alterar senha de usuário

userdel : remover usuário

su : acessar usuário

sudo : executar comando de elevação de privilégios

fdisk : gerenciar disco

mkfs : formatar partição

mount : montar partição

unmount : desmontar partição

3. Permissões de arquivos e pastas

Dono >  grupo > usuário (r=4 w=2 x=1)

4. Monitoramento do sistema operacional
5. Analise de logs nas aplicações
6. Gerenciamento de processos
7. Criação de Script

>Laboratório

vagrant up : cria máquina virtual
vagrant ssh : acesso servidor

mkdir brasil (crio pasta brasil)
ls (listo pastas)
cd brasil (acesso pasta brasil)
pwd (mostra diretório que eu me encontro)
mkdir minas-gerais bahia sao-paulo rio-de-janeiro (crio as pastas dos estados)
cd minas-gerais
touch belo-horizonte contagem (crio arquivos das cidades)
file belo-horizonte (me passa o que tem no arquivo)
vim belo-horizonte (para editar o arquivo)
:wq ou :x (salva arquivo)
cd .. (volta para o diretório anterior)
cd rio-de-janeiro (acesso pasta do rio de janeiro)
touch rio-de-janeiro niteroi (crio arquivos das cidades)
Repetir para memorizar

tree brasil (comando para ver a estrutura da pasta)
erro: não encontrado, para instalar execute apt install tree
sudo apt update : atualizar repositórios
sudo apt instal tree : instalar o comando
tree brasil : Mostra estrutura de pastas

cd brasil/bahia : vou direto para o diretório que quero
touch salvador porto-seguro
cd ..
cd ..
ls
tree brasil

cd minas-gerais
cp belo-horizonte /tmp (copio arquivo para pasta temporária)
cd /tmp
ls (mostra arquivo copiado)

cd - (volta para diretório anterior)

mv contagem nova-lima /tmp
ls /tmp/ (mostra arquivo movido renomeado)

find -name salvador (procuro arquivo pelo nome)
cd / : diretório raíz onde está por exemplo a pasta tmp

rm niteroi : remove arquivo
$ : indica privilégio do usuário

`# : privilégio root`
~ : home do usuário

>Laboratório Serviços

apt/yum (yum para redhat e apt para ubuntu) install ngninx (instalar nginx) - necessário privilégio de root
sudo su - cai no root
whoami - me passa qual usuário estou
apt install net-tools para utilizar ifconfig
ifconfig : pega informações de rede

apt install "Nome do pacote"

yum install mysql-server : instala mysql

service nginx status : para ver status do serviço instalado
systemctl status nginx : mesma função de ver status do serviço

service nginx stop : parar serviço
service nginx start : iniciar serviço

apt remove net-tools : para remover o pacote
mysql -uroot : entro no serviço

show databases: mostra tabelas do sql

cd/var/log : para ver logs

cd nginx
cat access .log : mostra logs no nginx - cat visualiza conteúdo do arquivo
tail -f "nome do arquivo" - vejo log do arquivo em tempo real

cd ~

>script

vim request.sh
#!/bin/bash
curl localhost
:wq

cat "nome do arquivo" |grep "Palavra" - filtro para texto

>permissões

chmod 675 bahia - altera permissões, retirando permissão de cd do dono

chmod 770 - permissão total para dono e grupo mas outros não podem nem ler o arquivo

ls -l : mostra permissões

>usuários

serviços também utilizam usuários no Linux

cat /etc/passwd - indica todos os usuários existentes

sudo su
useradd Saulo - crio usuário saulo

su Saulo - acesso usuário saulo
whoami - vejo que estou acessando usuário Saulo
para modificar de sh para bash - alterar arquivo etc/passwd pelo comando vim

passwd Saulo - para cadastrar senha de acesso ao usuário

>gerenciamento de disco

fdisk -l : lista discos da máquina

cd /dev/
ls
Mostra arquivos dentro dos discos 
sd normalmente é um disco (HD)
Primeiro hd : sda, segundo: sdb, terceiro : sdc

mkfs.xfs : para formatar partição

mount /dev/sdc1 / mnt/ : monto partição
df -h : mostro o que tem dentro da partição montada

unmount /mnt/ : desmonta partição

>Criação de Scripts

cd ~: para home
pwd: estou no /root

Quero criar Script para instalar pacote

vim instala-pacote.sh

#!/bin/bash

mkdir brasil
cd brasil
mkdir sao-paulo minas-gerais bahia rio-de-janeiro
cd sao-paulo
touch sao-paulo campinas
cd ../minas-gerais
touch belo-horizonte contagem
cd ../rio-de-janeiro
touch rio-de-janeiro niteroi
cd ../bahia
touch salvador porto-seguro
wq:

chmod 744 instala-pacote : dar permissão de execução
mv instala-pacote.sh geografia-brasil.sh : renomear

./geografia-brasil.sh : executa script

cat geografia-brasil.sh : para verificar conteúdo do script

Script de instalar pacotes

vim instala-pacotes.sh

#!/bin/bash
echo "instalando pacote $1" : para mostrar mensagem
apt install $1 : passo variável de ambiente

wq:

chmod 744 instala-pacotes.sh

./instala-pacotes.sh

me pede o nome do pacote por conta da variável de ambiente 

nginx

Aparece: "Instalando pacote nginx" e instala o pacote



