Para poder criar um novo projeto em Laravel é necessário ter instalado no computador o composer.

O código abaixo cria um projeto na pasta atual do bash

`composer create-project laravel/laravel example-app`

É possível realizar testes de intalação executando um servidor próprio, artisan, segue abaixo o código

`php artisan serve --host=0.0.0.0 --port=8000`

em --host com IP 0.0.0.0 a aplicação será acessada por qualquer maquina da rede, com o IP 127.0.0.1 só poderá ser acesso pelo localhost.
