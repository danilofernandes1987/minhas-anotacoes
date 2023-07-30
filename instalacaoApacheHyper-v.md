# Instalação de servidor Apache2 em um servidor Ubuntu 22.04 sendo executado em Hyper-v.

Este tutorial serve apenas como guia rápido para relizar instalação do paconte LAMP em um servidor Linux para fins de estudos e desenvolvimento. Jamais utilize este
manual para instalação a nível de produção, principalmente a parte da instalação e configuração do MariaDB. 

Foi instalado o Ubuntu na versão 22.04.

Corrigindo o timezone do servidor:

```bash
sudo timedatectl set-timezone Brazil/East
```

Instalando o aptitude para facilitar na instalação dos pacotes necessários:

```bash
sudo apt-get install aptitude
```

Instalando o php e suas dependencias:

```bash
sudo aptitude install php8.1 libapache2-mod-php8.1 php8.1-mysql php8.1-common php8.1-curl php8.1-json php8.1-xml php8.1-mbstring php8.1-gettext php8.1-pdo php8.1-gd php8.1-zip php8.1-soap php8.1-xmlrpc php8.1-intl php8.1-mysqlnd php8.1-cli php8.1-dev php8.1-zip libapache2-mod-php8.1 php8.1-curl php8.1-bz2 php-pear
```

Instalando o Mariadb:

```bash
sudo aptitude install mariadb-server
```

Configurando algumas váriaveis do php.ini:

```bash
sudo nano /etc/php/8.1/apache2/php.ini
```

```bash
date.timezone = America/Sao_Paulo  
upload_max_filesize = 200  
post_max_size = 200  
max_input_vars = 5000
```
Reiniciando o banco de dados para aplicação das alterações anteriores:

```bash
sudo systemctl restart mariadb
```

Alterando a senha de root do mariadb:

```mysql
ALTER USER 'root'@'localhost' IDENTIFIED BY 'MyNewPass';
```

Liberando acesso para rede externa ao banco de dados MariaDB:

```bash
sudo nano /etc/mysql/mariadb.conf.d/50-server.cnf
```

Altere a linha bind-address de 127.0.0.1 para 0.0.0.0.

Criando um usuário para acesso externo ao banco de dados:

```mysql
MariaDB [(none)]> grant all privileges on *.* to 'danilo'@'%' identified by 'minhasenha';
MariaDB [(none)]> flush privileges;  
MariaDB [(none)]> exit
```

## Configuração da rede do Hyper-v

Realizando alguns testes de usabilidade para estudos e laboratórios de Laravel foi verificado que o endereço de IP era alterado a cada reinicialização 
da máquina virtual, isso não é interessante em um ambiente de desenvolvimento onde é necessário configurar o VSCode para programação utilizando ssh.

Devido a esse problema, foram realizadas algumas pesquisas onde a solução mais fácil foi criar um adaptador de rede no Hyper-V, vSwitch Interno.

No gerenciador do Hyper-V clique sobre o Node e escolha a opção Gerenciador de Comutador Virtual. Selecione a opção Interno, verifique as informações na tela e por 
último, finalize a criação.

Será criada uma nova interface de rede na máquina física, atribua a ela um IP estático como por exemplo: 192.168.10.1/24.

Na máquina virtual é necessário adicionar mais um adaptador de rede, escolha no Comutador Virtual a Rede Interna. Após finalizado a adição, inicie a máquina virtual
e configure através do netplan a rede como estático.

```bash
sudo nano /etc/netplan/00-installer-config.yaml
```

```bash
# This is the network config written by 'subiquity'
network:
  ethernets:
    eth0:
      dhcp4: true
    eth1:
      addresses: [192.168.10.10/24]
      dhcp4: false
      optional: true
      nameservers:
            addresses: [192.168.10.1]
  version: 2
```
Finalizado a edição, testar e aplicar as configurações do netplan

```bash
sudo netplan try
```

```bash
sudo netplan apply
```