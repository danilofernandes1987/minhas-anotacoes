# Instalação de servidor Apache2 em um servidor Ubuntu 22.04 sendo executado em Hyper-v.
Foi instalado o Ubuntu na versão 22.04.
1. Corrigindo o timezone do servidor

`timedatectl set-timezone Brazil/East`

2. Instalando o apache2

`sudo apt install apache2`

1. Verificando o funcionamento do Apache

`sudo systemctl status apache2`

3. Instalando o aptitude para facilitar na instalação dos pacotes necessários

`sudo apt-get install aptitude`

4. Instalando o php e suas dependencias

`sudo aptitude install php8.1 libapache2-mod-php8.1 php8.1-mysql php8.1-common php8.1-curl php8.1-json php8.1-xml php8.1-mbstring php8.1-gettext php8.1-pdo php8.1-gd php8.1-zip php8.1-soap php8.1-xmlrpc php8.1-intl php8.1-mysqlnd php8.1-cli php8.1-dev php8.1-zip libapache2-mod-php8.1 php8.1-curl php8.1-bz2 php-pear`

5. Instalando o Mariadb

`sudo aptitude install mariadb-server`

6. Configurando algumas váriaveis do php.ini

`sudo nano /etc/php/8.1/apache2/php.ini`

date.timezone = America/Sao_Paulo  
upload_max_filesize = 200  
post_max_size = 200  
max_input_vars = 5000  