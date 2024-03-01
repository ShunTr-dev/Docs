```
use Cake\Core\Configure;

Configure::write('enviroment', 'development');

if(Configure::read('enviroment') == 'development') {
    /* DEVELOPMENT */
    $debug = true;

    //var/www/vhosts/dev.paymeter.primate.es/httpdocs/src/Controller/Api/ParkingsController.php
    Configure::write('parking_id_provided_to_API', '35');

    //var/www/vhosts/dev.paymeter.primate.es/httpdocs/src/Controller/RedsysController.php
    //var/www/vhosts/dev.paymeter.primate.es/httpdocs/src/Controller/Admin/PassesUsersController.php
    //var/www/vhosts/dev.paymeter.primate.es/httpdocs/src/Controller/Web/PassesUsersController.php
    Configure::write('tpv_key', 'sq7HjrUOBfKmC576ILgskD5srU870gJ7');
    Configure::write('tpv_url', 'https://sis-t.redsys.es:25443/sis/realizarPago');
} else {
    /* PRODUCTION */
    $debug = false;

    //var/www/vhosts/dev.paymeter.primate.es/httpdocs/src/Controller/Api/ParkingsController.php
    Configure::write('parking_id_provided_to_API', '10025');

    //var/www/vhosts/dev.paymeter.primate.es/httpdocs/src/Controller/RedsysController.php
    //var/www/vhosts/dev.paymeter.primate.es/httpdocs/src/Controller/Admin/PassesUsersController.php
    //var/www/vhosts/dev.paymeter.primate.es/httpdocs/src/Controller/Web/PassesUsersController.php
    Configure::write('tpv_key', '7914hSxLIDXodF3Tk7mpGr6hpTNo2KAm');
    Configure::write('tpv_url', 'https://sis.redsys.es/sis/realizarPago');
}
```