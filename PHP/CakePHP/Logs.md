```
use Cake\Log\Log;
Log::debug('Las firmas no coinciden.', ['scope' => ['gateway']]);

```
Para hacer que se haga un log en un archivo diferente:

-En config/app.php

```
'gateway' => [
  'className' => 'File',
  'path' => LOGS,
  'levels' => [],
  'scopes' => ['gateway'],
  'file' => 'gateway.log',
]

```
En el controlador:

```
use Cake\Log\Log;


Log::debug('Las firmas no coinciden.', ['scope' => ['gateway']]);
Log::debug('mensaje prueba', ['scope' => ['gateway']]);
//hay: Log::debug, warning, info, emergency, alert, critical, notice
```