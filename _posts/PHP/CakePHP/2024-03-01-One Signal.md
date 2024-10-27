---
title: One Signal
date: 2024-03-01 00:00:00 -100
categories: [PHP, CakePHP]
tags: [herramientas]
---

Función

```
/**
 * 
 * Función de enviado de notificaciones de One signal.
 *
 * @param (Array) $content -> dentro de un diccionario con los idiomas el mensaje de la notificación
 * @param (Array) $filters -> filtros de busqueda en one signal (user, group,...) hay que añadirlos como tags dentro de OneSignal
 * @param (CakeObj) $data_from_moncake -> datos que recibe la aplicación final
 * @return (Array) $return['succes'] (Boolean) -> true/false
 * @return (Array) $return['error'] (String)* -> Devuelve el error que dió one signal.
 *
 * @example 
 * $content      = array(
 *   "en" => 'The user ' . $client->username . ' has been warned',
 *   "es" => 'El usuario ' . $client->username . ' ha sido avisado'
 * );
 *
 * if($oneSignalMessage->group_id > 0){
 *  $filters = ["field" => "tag", "key" => "group", "relation" => "=", "value" => $id];
 *  $included_segments = null;
 * } else {
 *      $filters = null;
 *      $included_segments = 'All';
 * }
 *
 * $oneSignalResponse = $this->sendOnesignalNotifications($content, $filters, null, $included_segments);
 *
 * @since 18/1/2019 - Cakephp 3.6
 * @link https://documentation.onesignal.com/reference
 */
public function sendOnesignalNotifications ($content = null, $filters = null, $data_from_moncake = null, $included_segments = null) {
    //$this->autoRender = false;
    $this->loadModel('WebTexts');
    $one_signal_api_key = $this->WebTexts->find('all', ['conditions' => ['name' => 'one_signal_api_key'] ] )->first()->webtext;
    $one_signal_app_id = $this->WebTexts->find('all', ['conditions' => ['name' => 'one_signal_app_id'] ] )->first()->webtext;
    $fields = array(
        'app_id' => $one_signal_app_id,
        'data' => array(
            'data_from_moncake' => $data_from_moncake
        ),
        'contents' => $content
    );
    if ($filters != null) {
        $fields['filters'] = array($filters);
    } else {
        $fields['included_segments'] = [$included_segments];
    }
    
    $fields = json_encode($fields);
    
    $ch = curl_init();
    curl_setopt($ch, CURLOPT_URL, "https://onesignal.com/api/v1/notifications");
    curl_setopt($ch, CURLOPT_HTTPHEADER, array(
        'Content-Type: application/json; charset=utf-8',
        'Authorization: Basic ' . $one_signal_api_key
    ));
    curl_setopt($ch, CURLOPT_RETURNTRANSFER, TRUE);
    curl_setopt($ch, CURLOPT_HEADER, FALSE);
    curl_setopt($ch, CURLOPT_POST, TRUE);
    curl_setopt($ch, CURLOPT_POSTFIELDS, $fields);
    curl_setopt($ch, CURLOPT_SSL_VERIFYPEER, FALSE);
    
    $response = curl_exec($ch);
    if (strpos($response, 'error') !== false) {
        $return['success'] = false;
        $return['error'] = json_decode($response)->errors[0];
    } else {
        $return['success'] = true;
    }
    curl_close($ch);
    
    return $return;
}
```
Llamada

```
if($oneSignalMessage->group_id > 0){
  $filters = ["field" => "tag", "key" => "group", "relation" => "=", "value" => $oneSignalMessage->group_id];
  $included_segments = null;
} else {
  $filters = null;
  $included_segments = 'All';
}
$oneSignalResponse = $this->sendOnesignalNotifications($content, $filters, null, $included_segments);
```