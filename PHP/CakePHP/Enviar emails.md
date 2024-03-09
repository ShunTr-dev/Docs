# Enviar emails

Para enviar correos electrónicos en CakePHP, primero importamos las clases necesarias:

```php
use Cake\Mailer\Email;
use Cake\Routing\Router;
```

Luego, creamos una instancia del objeto `Email` y configuramos el correo electrónico:

```php
$email = new Email();
try {
    $res = $email->template('passwordrecovery', 'default')
                ->viewVars(['url' => Router::fullbaseUrl() . '/recoverys/passwordRecovery?hrp=' . $recovery->hash])
                ->emailFormat('html')
                ->to([$user->mail => $user->first_name . ' ' . $user->second_name])
                ->from($this->getWebText('email_contacto_admin'))
                ->subject(__('Asunto del email', 'admin'))
                ->send();
                
    $this->Flash->success(__('The email has been sent to ') . $user->mail);
} catch (Exception $e) {
    $this->Flash->error(__('Error when sending email.'));
    //echo 'Exception : ',  $e->getMessage(), "\n";
}
```

Este código configura el correo electrónico con una plantilla `passwordrecovery` y el formato `html`. Luego, se especifica el destinatario, el remitente y el asunto del correo electrónico. Finalmente, se envía el correo electrónico y se muestra un mensaje de éxito o error según corresponda.

Se proporciona un ejemplo adicional para enviar un correo electrónico en CakePHP:

```php
use Cake\Mailer\Email;
use Cake\Routing\Router;

$email = new Email();
try {
    $res = $email->template('passwordrecovery', 'default')
                ->viewVars(['url' => Router::fullbaseUrl() . '/web/recoverys/passwordRecovery?hrp=' . $recovery->hash])
                ->emailFormat('html')
                ->to([$user->mail => $user->first_name . ' ' . $user->second_name])
                ->from($this->getWebText('email_contacto_admin'))
                ->send();                

    $this->Flash->success(__('The email has been sent to ') . $user->mail);
} catch (Exception $e) {
    $this->Flash->error(__('Error when sending email.'));
    //echo 'Exception : ',  $e->getMessage(), "\n";
}
```

Este ejemplo sigue una estructura similar al primero, donde se configura y envía el correo electrónico, seguido de la manipulación de errores si ocurriera algún problema durante el envío.