Usar con el usuario installer -> contraseña Klap9woy

Ir al webroot (para que funcionen los bakes se tiene que hacer desde ahí) y ejecutar

```
bin/cake i18n extract 
```
Con esto arrancamos el motor de búsqueda de srt de i18n, va a preguntar :

Donde buscar, en SRC concretamente, si se añaden los cores del cake da ERROR (no en la creación del POT sino en la ejecución posterior en traducción).

Donde meter los POT, en src/Locale, que es donde están los POT en cake para que los use.

Las traducciones se deben meter en carpetas separadas como es / en / etc,.. luego en la carpeta interior se introduce el archivo generado con el editor como default.po (o la extensión que sea no me acuerdo si es esa o no)

Docu: https://book.cakephp.org/3.0/en/console-and-shells/i18n-shell.html

Crear la tabla I18n para idiomas

```
//crear tabla de i18n en cake php 3.5 - 3.6
CREATE TABLE i18n (
   id serial PRIMARY KEY,
   locale char(6) NOT NULL,
   model char(255) NOT NULL,
   foreign_key int(10) NOT NULL,
   field char(255) NOT NULL,
   content text
);
create UNIQUE INDEX I18N_LOCALE_FIELD on i18n(locale, model, foreign_key, field);
create INDEX I18N_FIELD on i18n(model, foreign_key, field);
```

```
<?php
use Migrations\AbstractMigration;
class CreateI18n extends AbstractMigration
{
    /**
     * Change Method.
     *
     * More information on this method is available here:
     * http://docs.phinx.org/en/latest/migrations.html#the-change-method
     * @return void
     */
    public function change()
    {
        $table = $this->table('i18n');
        $table->addColumn('locale', 'string', [
            'default' => null,
            'limit'   => 6,
            'null'    => false,
        ]);
        $table->addColumn('model', 'string', [
            'default' => null,
            'limit'   => 255,
            'null'    => false,
        ]);
        $table->addColumn('foreign_key', 'integer', [
            'default' => null,
            'limit'   => 11,
            'null'    => false,
        ]);
        $table->addColumn('field', 'string', [
            'default' => null,
            'limit'   => 255,
            'null'    => false,
        ]);
        $table->addColumn('content', 'text', [
            'default' => null,
            'null'    => false,
        ]);
        $table->addIndex(array('locale', 'model', 'foreign_key', 'field'), array('unique' => true, 'name' => 'I18N_PROMO_CODES_LOCALE_FIELD'));
        $table->addIndex(array('model', 'foreign_key', 'field'), array('unique' => false, 'name' => 'I18N_PROMO_CODES_FIELD'));
        $table->create();
    }
}
```
Cambiar versiones de PHP + I18n A ver, para cambiar la versión del servidor (esto va un poco como quiere)

```
nano ~/.bashrcphp
#export PATH=/opt/plesk/php/7.4/bin:$PATH
#export PATH=/usr/bin/php5.6/bin:$PATH
. ~/.bashrcphp -v

```
Traduccion i18n cake 1.4

```
Vale, se hace con:
Versión 5.6
En la carpeta: cd 
Con el comando ./cake i18n

```
Nueva versión

```
shopt -s expand_aliases
alias php="/usr/bin/php5.6"
php ./cake i18n
unalias php
```