# Migraciones en CakePHP

En CakePHP, las migraciones son una forma conveniente de gestionar la estructura de la base de datos de una aplicación. Aquí se presentan algunas operaciones y ejemplos comunes relacionados con las migraciones en CakePHP:

## Crear tabla en CakePHP

Para crear una nueva migración que incluya la creación de una tabla, puedes utilizar el siguiente comando:

```bash
bin/cake migrations create NombreDelArchivo name:string visible:boolean created modified
```

Una vez que se ha creado la migración, se puede ejecutar para aplicar los cambios en la base de datos:

```bash
bin/cake migrations migrate
```

Si necesitas deshacer una migración, puedes utilizar el siguiente comando:

```bash
bin/cake migrations rollback
```

## Generar archivos de modelo, controlador y vistas

Para generar rápidamente archivos de modelo, controlador y vistas relacionados con una tabla de la base de datos, puedes usar el comando `bake`. Puedes hacerlo por separado o generar todos los archivos a la vez:

```bash
bin/cake bake model Users
bin/cake bake controller Users
bin/cake bake template Users
bin/cake bake template Users add
bin/cake bake template Users edit
```

O simplemente:

```bash
bin/cake bake all Users
```

## Ejemplos de migraciones

A continuación se presentan algunos ejemplos de migraciones comunes en CakePHP:

### Creación de tabla

```php
class CreateFarms extends AbstractMigration {
    public function change()
    {
        $table = $this->table('farms');
        $table->addColumn('name', 'string', [
            'default' => null,
            'limit' => 255,
            'null' => false,
        ]);
        // Agregar más columnas según sea necesario...
        $table->create();
      
        // Ejemplo de añadir una clave externa
        $refTable = $this->table('farms');
        $refTable->addColumn('user_id', 'integer', ['signed' => 'disable'])
                 ->addForeignKey('user_id', 'users', 'id', ['delete' => 'CASCADE', 'update' => 'NO_ACTION'])
                 ->update();
    }
}
```

### Alterar tabla para añadir un nuevo campo

```php
class AlterImages extends AbstractMigration {
    public function change() {
        $table = $this->table('images');
        $table->addColumn('image', 'string', [
            'default' => null,
            'null' => true,
        ]);
        $table->addColumn('dir', 'string', [
            'default' => null,
            'null' => true,
        ]);
        $table->update();
    }
}
```

### Alterar tabla para modificar un campo existente

```php
public function up() {
    $table = $this->table('users');
    $table->changeColumn('postal_code', 'string', [
        'limit' => 255,
        'default' => null,
        'null' => true,
    ])->save();
}
```

### Eliminar un campo de una tabla

```php
class AlterClinicals extends AbstractMigration {
    public function up() {
        $table = $this->table('clinicals');
        $table->removeColumn('clinical_id')
              ->save();
    }
}
```

### Eliminar una tabla completa

```php
class DropAvoidancesDistancesImages extends AbstractMigration {
    public function change() {
        $table = $this->table('avoidance_distances_images');
        $table->drop();
    }
}
```

Estos ejemplos cubren las operaciones más comunes relacionadas con las migraciones en CakePHP. Puedes adaptarlos según las necesidades específicas de tu aplicación.