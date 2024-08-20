# Comentarios en PHP

Aquí se presenta un ejemplo de un comentario detallado para una función en PHP:

```php
/**
 *
 * Función de envío de notificaciones de OneSignal.
 *
 * @param (Array) $content - Un diccionario que contiene los mensajes de notificación en diferentes idiomas.
 * @param (Array) $filters - Filtros de búsqueda en OneSignal (usuarios, grupos, etc.), deben ser agregados como etiquetas dentro de OneSignal.
 * @param (CakeObj) $data_from_moncake - Datos recibidos por la aplicación final.
 * @return (Array) $return['succes'] (Boolean) - true/false
 * @return (Array) $return['error'] (String) - Devuelve el error que arrojó OneSignal.
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
 * $included_segments = 'All';
 * }
 * $oneSignalResponse = $this->sendOnesignalNotifications(content, $filters, null, $included_segments);
 * @since 18/03/2020 - CakePHP 3.6
 * @link https://documentation.onesignal.com/reference
 */
```
