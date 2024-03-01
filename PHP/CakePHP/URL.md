```
<?= $this->Url->build(['action' => 'add']);?>
Router::fullbaseUrl() . '/web/tickets/index/\
```
Referencia a la página desde la que se inició el proceso:

```
$this->redirect($this->referer());
```
Referencia a una accion del request

```
$this->request->getParam('prefix');
$this->request->getParam('controller');
$this->request->getParam('action');
```
Recoger elementos de URL por GET

```
$this->request->query('apartment')
```
Cambiar vista

```
$this->viewBuilder()->setLayout('ajax');
$this->viewBuilder()->template('index');
```
Leer sesion

```
$this->request->session()->read('User.group');
```
Obtener elementos del POST

```
$this->request->getData('code');
```
Traducciones

```
<?= $this->Translate->input('name', 'name_translations', $this, $serverLanguages, array('label'=> 'Name', 'type'=>'text') ) ?>
```