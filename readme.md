## DashBoard Generate CRUD

Caso queira criar um projeto do zero.
	
```
composer create-project --prefer-dist laravel/laravel nome_do_projeto "5.6.*"
```

Entre no projeto com o comando:
```
cd nome_do_projeto
```

Adicione no seu arquivo composer.json:
```
"require": {
    "infyomlabs/laravel-generator": "5.6.x-dev",
    "laravelcollective/html": "^5.6.0",
    "infyomlabs/adminlte-templates": "5.6.x-dev"
}
```

Se você quer gerar uma documentação para sua api em swagger annotations, você precisa instalar os seguintes pacotes:
```
"require": {
    "infyomlabs/swagger-generator": "dev-master",
    "appointer/swaggervel": "dev-master"
}
```

Se você quer usar opções de geração de tabela, você precisa instalar.
```
"require": {
    "doctrine/dbal": "~2.3"
}
```

Depois de adicionar pacotes, roda o seguinte comando:
```
composer update
```

Adicione os seguintes provisionadores de serviços em seu providers array em config/app.php:
```
Collective\Html\HtmlServiceProvider::class,
Laracasts\Flash\FlashServiceProvider::class,
Prettus\Repository\Providers\RepositoryServiceProvider::class,
\InfyOm\Generator\InfyOmGeneratorServiceProvider::class,
\InfyOm\AdminLTETemplates\AdminLTETemplatesServiceProvider::class, 
```

Adicione os seguintes apelidos para seu aliases array em config/app.php:
```
'Form'      => Collective\Html\FormFacade::class,
'Html'      => Collective\Html\HtmlFacade::class,
'Flash'     => Laracasts\Flash\Flash::class,
```

Rode o seguinte comando:
```
php artisan vendor:publish
Digite a opção '0'
```

Abra o app\Providers\RouteServiceProvider.php e altere o método mapApiRoutes:
```
Route::prefix('api')
    ->middleware('api')
    ->as('api.')
    ->namespace($this->namespace."\\API")
    ->group(base_path('routes/api.php'));
```

Execute o comando abaixo:
```
php artisan infyom:publish
```

Agora, você tem que habilitar o menu de opções in config/infyom/laravel_generator.php. Fazendo menu option para true.

Adicione os seguinites pacotes em seu composer.json.
```
"require": {
    "infyomlabs/generator-builder": "dev-master"
} 
```

Execute o comando abaixo:
```
composer update
```

Adicione os seguintes provedores de serviços dentro de providers array em config/app.php:
```
\InfyOm\GeneratorBuilder\GeneratorBuilderServiceProvider::class, 
```

Execute o comando abaixo:
```
php artisan vendor:publish 
Digite a opção '0'
```

Ele irá criar config/infyom/generator_builder.php em cada views para o gerador especifico.

Execute o seguinte comenado:
```
php artisan infyom.publish:generator-builder 
```

Publique as seguintes rotas no arquivo routes.php:
```	Route::get('generator_builder', '\InfyOm\GeneratorBuilder\Controllers\GeneratorBuilderController@builder');
	Route::get('field_template', '\InfyOm\GeneratorBuilder\Controllers\GeneratorBuilderController@fieldTemplate');
	Route::post('generator_builder/generate', '\InfyOm\GeneratorBuilder\Controllers\GeneratorBuilderController@generate'); 
```

Execute o seguinte comando:
```
php artisan infyom.publish:generator-builder --views 
```

Depois, mude arquivo de configuração config/infyom/generator_builder.php.
```
mude 
	'builder' => 'generator-builder::builder' 
para 
	'builder' => 'infyom.generator-builder.builder'

mude 
	'field-template' => 'generator-builder::field-template' 
para 
	'field-template' => 'infyom.generator-builder.field-template'
```

Execute o comando abaixo:
```
php artisan infyom.publish:layout 
```

Crie sua base de dados 'name_data_base' e mude as configurações no .env ou config/database.php.

Adicione no arquivo app\Providers\AppServiceProvider.php
```
use Illuminate\Support\Facades\Schema;

dentro de register() -> Schema::defaultStringLength(191);
```

Execute o comando:
```
php artisan migrate
```


