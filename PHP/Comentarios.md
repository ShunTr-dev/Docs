```
/**
 *
 * Función de enviado de notificaciones de One signal.
 * @param (Array) $content -> dentro de un diccionario con los idiomas el mensaje de la notificación
 * @param (Array) $filters -> filtros de busqueda en one signal (user, group,...) hay que añadirlos como tags dentro de OneSignal
 *
 * @param (CakeObj) $data_from_moncake -> datos que recibe la aplicación final
 * @return (Array) $return['succes'] (Boolean) -> true/false
 * @return (Array) $return['error'] (String)* -> Devuelve el error que dió one signal.
 * @example
 * $content = array(
 * "en" => 'The user ' . $client->username . ' has been warned',
 * "es" => 'El usuario ' . $client->username . ' ha sido avisado'
 * );
 * if($oneSignalMessage->group_id > 0){
 * $filters = ["field" => "tag", "key" => "group", "relation" => "=", "value" => $id];
 * $included_segments = null;
 * } else {
 * $filters = null;
 * 
 * $included_segments = 'All';
 * 
 * }
 * oneSignalResponse = $this->sendOnesignalNotifications(content, $filters, null, $included_segments);
 * @since 18/03/2020 - Cakephp 3.6
 * @link https://documentation.onesignal.com/reference 
 */
```