# Aula sobre testes com Laravel

### Autor: Eduardo Dalla Vecchia

Para acompanhar a aula é necessário Uma instalação do laravel 8 e um banco de dados de sua preferência

Se já tem uma aplicação rodando com estes requisitos, vá direto [ao passo 2](https://github.com/swalker2/aula-laravel-tests/blob/main/README.md#passo-2-preparando-para-a-aula)

Dica: Cria aliases para rodar os comandos mais rapidamente:
```bash
alias sail='./vendor/bin/sail'
alias art='sail artisan'
```

### Passo 1: Criando o projeto

Certifique-se que não existe um servidor http na porta 80 ativo, se houver, finalize para executar esta aplicação

```bash
# Download e instalação da aplicação
curl -s "https://laravel.build/aula-laravel-tests" | bash

# Acesse a pasta
cd aula-laravel-tests

# Inicializando a aplicação
./vendor/bin/sail up
```

### Passo 2: Preparando para a aula

- Substitua `./vendor/bin/sail` por `php` caso não estiver usando laravel sail  

1. Adicione um model e migration para os testes unitários
   ```bash
   ./vendor/bin/sail artisan make:model Invoice -m
   ```
   - Adicione os seguintes campos na migration create_invoices_table 
    ```php
    public function up()
    {
        Schema::create('invoices', function (Blueprint $table) {
            $table->id();
            $table->string('code')->nullable(); // vamos fazer o gerador ;) 
            $table->unsignedInteger('buyer_id');
            $table->string('buyer_email');
            $table->unsignedInteger('price'); // vamos converter para float
            $table->unsignedTinyInteger('status');
            $table->timestamps();
        });
    } 
   ```

2. Instale e inicialize o laravel breeze
    ```bash
    ./vendor/bin/sail composer require laravel/breeze --dev
    # vamos fazer testes referente à funcionalidades já prontas do login
    ./vendor/bin/sail artisan breeze:install
    ./vendor/bin/sail npm i
    ./vendor/bin/sail npm run dev
    ```
3. Rode as migrations
    ```bash
   ./vendor/bin/sail artisan migrate 
   ```

---

Tudo pronto, verifique se está tudo funcionando e vejo vocês amanhã :)
