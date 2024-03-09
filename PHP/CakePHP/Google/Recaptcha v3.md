## Recaptcha en CakePHP

### HTML CakePHP

```html
<style type="text/css">
    .grecaptcha-badge { visibility: hidden; }
    html { overflow: hidden !important; }
</style>
<form action="" id="login-form" class="smart-form client-form" method="post">
    <header>
        <?= __('Sign In') ?>
    </header>
    <fieldset>
        <section>
            <label class="label"><?= __('User') ?></label>
            <label class="input"> <i class="icon-append fa fa-user"></i>
                <input type="username" name="username">
                <b class="tooltip tooltip-top-right"><i class="fa fa-user txt-color-teal"></i> <?= __('Please enter username') ?></b></label>
        </section>
        <input type="hidden" name="google_captcha_v3" value="" id="google_captcha_v3" />
        <section>
            <label class="label"><?= __('Password') ?></label>
            <label class="input"> <i class="icon-append fa fa-lock"></i>
                <input type="password" name="password">
                <b class="tooltip tooltip-top-right"><i class="fa fa-lock txt-color-teal"></i><?= __('Enter your password') ?> </b> </label>
            <div class="note">
                <a href="/recoverys/recovery"><?= __('Forgot password?') ?></a>
            </div>
        </section>
        <section>
            <label class="checkbox">
                <input type="checkbox" name="remember" checked="">
                <i></i><?= __('Stay signed in') ?></label>
        </section>
    </fieldset>
    
</form>
<div class="g-recaptcha" data-sitekey="<?= $this->Webtext->getText('google_captcha_v3_key_client'); ?>"></div>
<script src="https://www.google.com/recaptcha/api.js?onload=ReCaptchaCallbackV3&render=<?= $this->Webtext->getText('google_captcha_v3_key_client'); ?>"></script>
<script>
    ReCaptchaCallbackV3 = function() {
        grecaptcha.ready(function() {
            grecaptcha.execute("<?= $this->Webtext->getText('google_captcha_v3_key_client'); ?>").then(function(token) {
                $('#google_captcha_v3').val(token);
                $('#login-form').attr('action', '/users/login');
                $('#login-form').append('<footer id="footer"><button type="submit" class="btn btn-primary" onclick="convert();"><?= __('Sign in') ?></button></footer>');
            });
        });
    };
    function convert() {
        var srch=document.getElementById("username");
        str = srch.value;
        srch.value=str.toLowerCase();
    }
</script>
```

### PHP CakePHP

```php
public function recaptchav3($token = null) {
    $score = null;
    $this->loadModel('WebTexts');
  
    $recaptcha_url = 'https://www.google.com/recaptcha/api/siteverify'; 
    $recaptcha_secret = $this->WebTexts->find('all')->where(['WebTexts.name' => 'google_captcha_v3_key_server'])->first()->webtext;
    $recaptcha = json_decode(file_get_contents($recaptcha_url . '?secret=' . $recaptcha_secret . '&response=' . $token));
    if($recaptcha->success == 'true'){
        return $recaptcha->score;
    } else {
         return $this->redirect($this->Auth->redirectUrl());
    }
}
//call it...
if($this->recaptchav3($this->request->getData('google_captcha_v3')) > 0.7 ){}
```

Este documento proporciona una integración de Recaptcha en una aplicación CakePHP. La sección HTML CakePHP incluye un formulario de inicio de sesión con campos de usuario y contraseña, así como un área para el Recaptcha. El script JavaScript maneja la ejecución de Recaptcha y la manipulación del formulario. En la sección PHP CakePHP, se proporciona una función para verificar el token Recaptcha y se muestra cómo llamarla en el código.