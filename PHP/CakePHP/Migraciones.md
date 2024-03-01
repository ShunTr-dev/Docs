Crear tabla en cake (todo desde el webpath)

```
bin/cake migrations create NombreDelArchivo name:string visible:boolean created modified
```
- Se crea un archivo en /config/migrations
Para ejecutar la migración debemos ejecutar:

```
bin/cake migrations migrate 
```
Si ponemos una configuración no deseada podemos poner este comando para deshacer la migración.

```
bin/cake migrations rollback
```
Para hacer los bakes de los archivos podemos ejecutar todo por separado:

```
bin/cake bake model Users
bin/cake bake controller Users
bin/cake bake template Users
bin/cake bake template Users add
bin/cake bake template Users edit
```
O podemos generalo todo de una vez

```
bin/cake bake all Users
```

Ejemplo de migración Creación

```
class CreateFarms extends AbstractMigration {
    public function change()
    {
        $table = $this->table('farms');
        $table->addColumn('name', 'string', [
            'default' => null,
            'limit' => 255,
            'null' => false,
        ]);
        $table->addColumn('cows', 'integer', [
            'default' => 0,
            'limit' => 11,
            'null' => false,
        ]);
        $table->addColumn('surface_area', 'float', [
            'default' => 0,
            'null' => true,
        ]);
        $table->addColumn('last_audit', 'datetime', [
            'default' => null,
            'null' => true,
        ]);
        $table->addColumn('created', 'datetime', [
            'default' => null,
            'null' => false,
        ]);
        $table->addColumn('modified', 'datetime', [
            'default' => null,
            'null' => false,
        ]);
        $table->create();
      
        $refTable = $this->table('farms');
        $refTable->addColumn('user_id', 'integer', array('signed' => 'disable'))
                 ->addForeignKey('user_id', 'users', 'id', array('delete' => 'CASCADE', 'update' => 'NO_ACTION'))
                 ->update();
    }
}
```

Ejemplo de Alter de meter un campo nuevo:

```
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
Ejemplo de hacer un ALTER de un campo EXISTENTE:

```
public function up() {
        $table = $this->table('users');
        $table->changeColumn('postal_code', 'string', [
            'limit' => 255,
            'default' => null,
            'null' => true,
        ])->save();
    }
```

Ejemplo creación Borrar un campo:

```
class AlterClinicals extends AbstractMigration {
    public function up() {
        $table = $this->table('clinicals');
        $table->removeColumn('clinical_id')
              ->save();
    }
}
```

Ejemplo de Drop Database

```
class DropAvoidancesDistancesImages extends AbstractMigration {
    public function change() {
        $table = $this->table('avoidance_distances_images');
        $table->drop();
    }
}
```