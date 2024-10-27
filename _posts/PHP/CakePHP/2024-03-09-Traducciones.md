---
title: Traducciones
date: 2024-03-09 00:00:00 -100
categories: [PHP, CakePHP]
tags: [herramientas]
---

# Traducciones en CakePHP

Para iniciar el proceso de extracción de las traducciones, es necesario dirigirse al directorio raíz del proyecto (webroot) y ejecutar el siguiente comando:

```bash
bin/cake i18n extract
```

Este comando activa el motor de búsqueda de traducciones i18n. Durante la ejecución, se solicitarán ciertas configuraciones:

- **Dónde buscar:** Se debe especificar la carpeta "SRC". Es importante tener en cuenta que si se añaden los cores del Cake, puede producirse un ERROR durante la ejecución posterior en la traducción.
  
- **Dónde colocar los archivos POT:** Se recomienda colocar los archivos POT en la carpeta `src/Locale`, que es la ubicación predeterminada en CakePHP para su uso.

Las traducciones deben organizarse en carpetas separadas, como `/en`, `/es`, etc. Dentro de cada carpeta de idioma, se debe colocar el archivo generado, generalmente denominado `default.po` (o con la extensión correspondiente).

Para obtener más información y detalles sobre este proceso, se puede consultar la documentación oficial de CakePHP: [Documentación sobre i18n Shell](https://book.cakephp.org/3.0/en/console-and-shells/i18n-shell.html)

## Creación de la tabla I18n para idiomas

Para crear la tabla I18n en CakePHP 3.5 - 3.6, se deben ejecutar las siguientes consultas SQL:

```sql
CREATE TABLE i18n (
   id serial PRIMARY KEY,
   locale char(6) NOT NULL,
   model char(255) NOT NULL,
   foreign_key int(10) NOT NULL,
   field char(255) NOT NULL,
   content text
);
CREATE UNIQUE INDEX I18N_LOCALE_FIELD ON i18n(locale, model, foreign_key, field);
CREATE INDEX I18N_FIELD ON i18n(model, foreign_key, field);
```

O utilizando una migración de Phinx:

```php
<?php
use Migrations\AbstractMigration;

class CreateI18n extends AbstractMigration
{
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

## Cambiar versiones de PHP e i18n

Para cambiar la versión de PHP y el entorno i18n, se pueden seguir los siguientes pasos:

1. Editar el archivo `~/.bashrcphp` utilizando un editor de texto como `nano`:

```bash
nano ~/.bashrcphp
```

2. Seleccionar la versión de PHP deseada comentando/descomentando las líneas que definen la ruta del ejecutable de PHP:

```bash
#export PATH=/opt/plesk/php/7.4/bin:$PATH
#export PATH=/usr/bin/php5.6/bin:$PATH
```

3. Recargar el archivo de configuración `.bashrcphp`:

```bash
. ~/.bashrcphp
```

4. Verificar la versión de PHP actualmente configurada:

```bash
php -v
```

Para realizar la traducción i18n en CakePHP 1.4, se debe ejecutar el siguiente comando en la versión 5.6 de PHP, ubicado en la carpeta correspondiente:

```bash
./cake i18n
```

Para una versión más reciente, se puede utilizar el siguiente script:

```bash
shopt -s expand_aliases
alias php="/usr/bin/php5.6"
php ./cake i18n
unalias php
```

Estos son los pasos generales para cambiar las versiones de PHP e iniciar el proceso de traducción i18n en diferentes versiones de CakePHP.