```
//on cake
$invoice->end_date->format('d-m-Y');


use Cake\I18n\Time;
$contract->severance_date = new Time(date('Y-m-d'));

```

```
date("Y-m-d 00:00:00", strtotime("now"));
date("Y-m-d 00:00:00", strtotime("-30 day"));
date('Y-m-d', strtotime($Date. ' + 1 days'));

```

```
date("Y-m-d H:i:s");

```
Diferencia en segundos entre dos fechas:

```
$date1 = new \DateTime($ticket->input_date->format('Y-m-d H:i:s'));
$date2 = new \DateTime($ticket->output_date->format('Y-m-d H:i:s'));
$diff_seconds = $date1->diff($date2);
$seconds_worked_today += ( ( ($diff_seconds->d * 24 ) * 60 ) * 60) + ( ( $diff_seconds->h * 60 ) * 60) + ( $diff_seconds->i * 60 ) + $diff_seconds->s;

```

```
$time = strtotime('10/16/2003');


$newformat = date('Y-m-d',$time);
=> date('Y-m-d H:i:s',strtotime($start_date));

```
Función para pasar de segundos a horas:minutos:segundos

```
function seconds_converter($total_seconds) {
    $hours = floor( $total_seconds / 3600 );
    $minutes = floor( ($total_seconds - ( $hours * 3600 )) / 60);
    $seconds = $total_seconds - ( $hours * 3600 ) - ( $minutes * 60 );
    return $hours . ':' . $minutes . ':' . $seconds . 's';
}

```
Con CAKEPHP

```
<?php
    use Cake\I18n\Time;
?>
Time::now()->modify('-1 year');
```