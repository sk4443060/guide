Pure Custom Laravel Auth Implementation

🧱 STEP 1: Fresh Laravel Installation

    composer create-project laravel/laravel your-project-name
    cd custom-auth
    php artisan serve

🧩 STEP 2: Create Database and Update .env
    Now open .env file and set:

    DB_DATABASE=custom_auth_db
    DB_USERNAME=root
    DB_PASSWORD=

🧱 STEP 3: Create Migration for Users Table (Already there)
    By default Laravel has a migration file:
    database/migrations/2014_10_12_000000_create_users_table.php
    Check that it includes:

    $table->id();
    $table->string('name');
    $table->string('email')->unique();
    $table->timestamp('email_verified_at')->nullable();
    $table->string('password');
    $table->rememberToken();
    $table->timestamps();

   Then migrate:

    php artisan migrate

  ✅ Database ready.

Implement the other part:
https://github.com/sk4443060/guide/blob/main/Create%20Auth%20Controllers%20Pure%20Custom%20Laravel%20Auth%20Implementation.md
    
