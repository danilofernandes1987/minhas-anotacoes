Para poder criar um novo projeto em Laravel é necessário ter instalado no computador o composer.

O código abaixo cria um projeto na pasta atual do bash

```bash
composer create-project laravel/laravel example-app`
```

É possível realizar testes de intalação executando um servidor próprio, artisan, segue abaixo o código

```bash
php artisan serve --host=0.0.0.0 --port=8000`
```

Em --host com IP 0.0.0.0 a aplicação será acessada por qualquer maquina da rede, com o IP 127.0.0.1 só poderá ser acesso pelo localhost.

## Criando Controller com Artisan.
O Artisan proporciona a possibilidade de criar os Controllers com o comando:

```bash
php artisan make:controller NomeController`
```

Existe uma convenção para nomenclaturas de metodos de um Controller que pode ser conferido [neste link](https://laravel.com/docs/10.x/controllers).


### Dicas
Para usar alguns comandos e o Artisan about é necessário instalar o *php-mbstring*

Para realizar clone de um repositório git, é necessário executar os seguintes comandos para baixar as bibliotecas e dependencias.

```bash
composer install --no-scripts
```

```bash
cp .env.example .env
```

```bash
php artisan key:generate
```