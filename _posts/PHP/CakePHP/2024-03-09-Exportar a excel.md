---
title: Exportar a excel
date: 2024-03-09 00:00:00 -100
categories: [PHP, CakePHP]
tags: [php, cakephp, excel]
---

# Exportar a Excel en CakePHP

A continuación se presenta un ejemplo de cómo exportar datos a un archivo Excel en CakePHP. Este método exporta los datos de los tickets a un archivo CSV.

```php
public function exportOrders() {
    $this->autoRender = false;
    
    // FILTROS
    //$apartment = $this->request->query('apartment');
    //$type = $this->request->query('type');
    //$provider = $this->request->query('provider');
    //$start_date = $this->request->query('start_date');
    //$end_date = $this->request->query('end_date');

    // CONDICIONES (FILTROS)
    $parking = $this->request->query('p');
    $start_date = $this->request->query('start_date');
    $end_date = $this->request->query('end_date');
    $conditions = array();

    if($start_date){
        $conditions['Ordersrs.date_order::date >'] = $this->formatDateTime($start_date);
    }
    
    if($end_date){
        $conditions['Tickets.date_order::date <='] = $this->formatDateTime($end_date);
    }
    
    if($parking){
        $conditions['Tickets.parking_id'] = $parking;
    }

    $tickets = $this->Tickets->find('all', [
        'contain' => ['Parkings', 'Tariffs', 'Users', 'Vehicles'], 
        'order' => ['input_date' => 'DESC'], 
        'conditions' => [$conditions]
    ]);

    if ($tickets->count() > 0) {
        $data = array();
        foreach($tickets as $ticket){
            $line = array();
        
            //$line['total'] = utf8_decode(str_replace('€','EUR',Number::currency($ticket->total, 'EUR')));
            $line['total'] = utf8_decode($ticket->total . ' EUR');
            $line['input_date'] = utf8_decode($ticket->input_date);
            $line['output_date'] = utf8_decode($ticket->output_date);
            $line['parking'] = utf8_decode($ticket->parking->name);
            $line['vehicle'] = utf8_decode($ticket->vehicle->plate);
            
            $data[] = $line;
        }
    } else {
        $data = array();
        $line = array();
    
        $line['total'] = utf8_decode('');
        $line['input_date'] = utf8_decode('');
        $line['output_date'] = utf8_decode('');
        $line['parking'] = utf8_decode('');
        $line['vehicle'] = utf8_decode('');
        $line['Total'] = utf8_decode('');
        
        $data[] = $line;
    }

    header("Pragma: public"); 
    header("Expires: 0");
    header("Cache-Control: must-revalidate, post-check=0, pre-check=0");
    header("Content-Type: application/force-download");
    header("Content-Type: application/octet-stream");
    header("Content-Type: application/download");
    header("Content-Disposition: attachment;filename=gastos.csv");
    header("Content-Transfer-Encoding: binary");
    ob_start();
    
    $df = fopen("php://output", 'w');
    
    fputcsv( $df, array_keys( $data[0] ),";" );
    
    foreach ($data as $row) {
        fputcsv($df, $row, ";");
    }
       
    fclose($df);
       
    echo ob_get_clean();
    die();
}
```

Este método toma los parámetros de filtro de la URL y genera un archivo CSV con los datos de los tickets. Luego, los encabezados de respuesta se configuran para que el navegador descargue el archivo CSV automáticamente.