```
use Cake\Mailer\Email;
use Cake\Routing\Router;
```

```
$email = new Email();
try {
    $res = $email->template('passwordrecovery', 'default')
                ->viewVars(['url' => Router::fullbaseUrl() . '/recoverys/passwordRecovery?hrp=' . $recovery->hash])
                ->emailFormat('html')
                ->to([$user->mail => $user->first_name . ' ' . $user->second_name])
                ->from($this->getWebText('email_contacto_admin'))
                ->subject( __('Asunto del email', 'admin') )
                ->send();                
    $this->Flash->success(__('The email has been sent to ') . $user->mail);
} catch (Exception $e) {
    $this->Flash->error(__('Error when sending email.'));
    //echo 'Exception : ',  $e->getMessage(), "\n";
}
```