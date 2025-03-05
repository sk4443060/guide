<!-- FILAMENT SETUP WITH LARAVEL -->
[#]Installation
    composer require filament/filament:"^3.2" -W
    php artisan filament:install --panels
    [YOU_WILL_NOTICE] app/Providers/Filament/AdminPanelProvider.php

[#]Create a user (Open /admin in your web browser, sign in, and start building your app!)
    php artisan make:filament-user
    [FOLLOW_THE_GUIDE_AND_CREATE_USER]

<!-- WORKING WITH FILAMENT -->
[#] Run the folloing command to make/create "Product MODAL, CONTROLLER WITH RESOURCE (-mcr)"
    php artisan make:model Product -mcr
[#] Now run the following command to create filament resource
    php artisan make:filament-resource Category