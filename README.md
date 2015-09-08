Add package to `package.json`
```json
"repositories": [
    {
        "type": "vcs",
        "url": "https://github.com/rafis/schema-extended"
    }
],
"require": {
    "laravel/framework": "5.0.*",
    "rafis/schema-extended": "~1.0"
},
```

Do not forget to run `composer install` after modifying `package.json`.

Replace "alias" in the configuration file `config/app.php`:
```php
'aliases' => array(
    ...
    // 'Schema' => 'Illuminate\Support\Facades\Schema',
    'Schema'    => 'SchemaExtended\Schema',
),
```

Use new features in migrations:
```php
Schema::create('tests', function ($table) {
    $table->increments('id');
    $table->string('description', 1000)->collate('utf8_general_ci');
    $table->binary('md5', 16); // will use BINARY(16) instead of BLOB
    $table->binary('sha1', 20); // will use BINARY(20) instead of BLOB
    $table->boolean('enabled')->comment('columns comment');
    $table->comment = 'table comment';
});
```