# Monitorización de usuarios en CakePHP

## Controlador del elemento

```php
/**
 * Se ejecuta DESPUÉS de cada acción del controlador y DESPUÉS de que se complete el renderizado. Este es el ÚLTIMO método del controlador en ejecutarse.
 *
 * @since 05/03/2020 - Cakephp 3.6
 * @link https://book.cakephp.org/3/en/controllers.html#controller-callback-methods
 */
public function afterFilter(Event $event) {
    $save = false;
    if ($this->request->session()->check('User')) {
        /**
         * Función para guardar las acciones realizadas por los usuarios. 
         * (Se ejecuta por controlador)
         * Llama a userMonitoringVarInit() que se encuentra en el AppController para inicializar la variable.
         *
         * @since 18/03/2020 - Cakephp 3.6
         */
        $newAction = $this->userMonitoringVarInit();
        switch ($this->request->getParam('action')) {
            case "index":
                $newAction->type = 1;
                $newAction->entity_name = null;
                $newAction->description = null;
                //$save = true;
                break;
            case "view":
                $newAction->type = 1;
                $newAction->entity_name = null;
                $newAction->description = null;
                //$save = true;
                break;
            case "add":
                $newAction->type = 2;
                $newAction->entity_name = null;
                $newAction->description = null;
                //$save = true;
                break;
            case "singleToPdf":
                $newAction->type = 1;
                $newAction->entity_name = null;
                $newAction->description = null;
                //$save = true;
                break;
            case "multipleToPdf":
                if (isset($this->viewVars['access'])) {
                    $newAction->type = 2;
                    $newAction->entity_name = 'Acceso: ' . $this->viewVars['access']->worker->name . ' ' . $this->viewVars['access']->worker->second_name;
                    //$newAction->description = $this->request->session()->read('User.name_complete') . ' añadió el acceso de ' . $this->viewVars['access']->worker->name . ' ' . $this->viewVars['access']->worker->second_name;
                    $newAction->description = $this->request->session()->read('User.name_complete') . ' añadió un acceso';
                    $save = true;
                }
                break;
            case "edit":
                if ($this->request->is(['patch', 'post', 'put'])) {
                    $newAction->type = 2;
                    $newAction->entity_name = 'Acceso: ' . $this->viewVars['access']->worker->name . ' ' . $this->viewVars['access']->worker->second_name;
                    $newAction->description = $this->request->session()->read('User.name_complete') . ' modificó un acceso de ' . $this->viewVars['access']->worker->name . ' ' . $this->viewVars['access']->worker->second_name . ' en la habitación ' . $this->viewVars['access']->room->name ;
                    $save = true;
                }
                break;
            case "delete":
                if ($this->request->is(['patch', 'post', 'put'])) {
                    $newAction->type = 4;
                    $newAction->entity_name = 'Acceso: ' . $this->viewVars['access']->worker->name . ' ' . $this->viewVars['access']->worker->second_name;
                    $newAction->description = $this->request->session()->read('User.name_complete') . ' eliminó el acceso de ' . $this->viewVars['access']->worker->name . ' ' . $this->viewVars['access']->worker->second_name . ' a la habitación ' . $this->viewVars['access']->room->name ;
                    $save = true;
                }
                break;
        }
        if ($save) {
            $this->UserMonitoring->save($newAction);
        }
    }
}
```

## AppController

```php
/**
 * 
 * Función de inicialización de la variable que guarda los datos de monitorización
 *
 * @return (Cake Obj) $newAction->user_id (Integer) -> Id de usuario
 *                    $newAction->url (String) -> URL de acceso
 *                    $newAction->ip (String) -> IP desde la que se hizo la petición
 *                    $newAction->request (String) -> Petición (actualmente en null)
 *                    $newAction->agent (String) -> User agent
 *                    $newAction->date (Datetime) -> Fecha de modificación
 *                    $newAction->type (Integer) -> Tipo de acción añadir/editar/borrar
 *                    $newAction->entity_name (String) -> Nombre del elemeto que se está modificando
 *                    $newAction->description (String) -> Descripción de la acción realizada
 *
 * @since 05/03/2020 - Cakephp 3.6
 */
public function userMonitoringVarInit() {
    if ($this->request->session()->check('User')) {
        //Ejecución cuando un usuario esta logueado.
        //Inicializamos con valores el objeto que contiene los datos el usuario para su monitorización de acciones.
        $this->loadModel('UserMonitoring');
        $newAction = $this->UserMonitoring->newEntity();
        $newAction->user_id = $this->request->session()->read('User.id');
        $newAction->url = $_SERVER[ 'REQUEST_URI' ];
        $newAction->ip = $this->request->clientIp();
        $newAction->request = null;
        $newAction->agent = env('HTTP_USER_AGENT');
        $newAction->date = time();
        $newAction->entity_name = null;
        $newAction->description = null;
        $newAction->type = 1;
        /**********************************
            TYPE OPTIONS
            1 => VER / LEER
            2 => AÑADIR
            3 => EDITAR
            4 => ELIMINAR
        **********************************/
        return $newAction;
    }
}
```

Estos fragmentos de código permiten monitorear las acciones realizadas por los usuarios en CakePHP. La función `afterFilter` en el controlador se encarga de registrar las acciones realizadas después de cada acción del controlador, mientras que la función `userMonitoringVarInit` en el `AppController` inicializa las variables necesarias para el registro de estas acciones.