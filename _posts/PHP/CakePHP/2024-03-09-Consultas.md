---
title: Consultas
date: 2024-03-09 00:00:00 -100
categories: [PHP, CakePHP]
tags: [php, cakephp, consultas]
---

Estos son algunos ejemplos de consultas complejas en CakePHP:

1. **Consulta con condiciones anidadas:**
```php
$workers = $this->Workers->find('all', [
    'conditions' => [
        'Workers.id IN' => $this->Contracts->find('all', [
            'conditions' => [
                'OR' => [
                    'category_ciqus_id IN' => $conditions,
                    ['end_date is null', 'category_ciqus_id IN' => $conditions],
                    ['end_date >' => date('Y-m-d'), 'category_ciqus_id IN' => $conditions]
                ]
            ]
        ])->select('worker_id')
    ]
]);
```

2. **Consulta con condiciones simples:**
```php
$workers = $this->Workers->find('all', [
    'conditions' => [
        'Workers.id IN' => $this->Contracts->find('all')->select('worker_id')->where(['end_date is null', 'category_ciqus_id IN' => $categories_ids])->orWhere(['end_date >' => date('Y-m-d'), 'category_ciqus_id IN' => $categories_ids])
    ]
]);
```

3. **Consulta con funciones de agregación (SUM/AVG/COUNT):**
```php
$query = $this->WorkingDays->find('all', [
    'conditions' => [
        'user_id' => $user->id,
        'work_day >=' => $start_date,
        'work_day <=' => date("Y-m-t", strtotime($start_date)) 
    ] 
]);
$workingDays_calculated = $query->select([
    'total_seconds' => $query->func()->sum('WorkingDays.total_seconds'),
    'avg_seconds' => $query->func()->sum('WorkingDays.total_seconds'),
    'total_days_worked' => $query->func()->sum('WorkingDays.id')
])->first();
```

4. **Consulta con SQL directo:**
```php
use Cake\Datasource\ConnectionManager;
$connection = ConnectionManager::get('default');
$total_earnings_tickets = $connection
    ->execute(
        'SELECT (SUM(total_tax)) AS "total_tax", (SUM(total_discounted)) AS "discount", (SUM(total_without_tax)) AS "total_without_tax", (SUM(total)) AS "total_calculated" FROM tickets WHERE (parking_id = ' . $parking->id . ' AND status = 1 AND date(output_date) >= \'' . date('Y-m-d', strtotime($firstDayOfMonth) ) . '\' AND date(output_date) < \'' . date('Y-m-d', strtotime($lastDayOfMonth) ) . '\'::date)'
    )
    ->fetchAll('assoc')[0];
```

5. **Consulta con agrupación y condiciones relacionadas:**
```php
$contracts_by_sexes = $this->Workers->find('all', [
    'contain' => ['Sexes'],
    'group' => 'Sexes.name',
    'fields' => [
        "count_contracts_sex" => "COUNT(Sexes.name)", 
        'name' => 'Sexes.name'
    ]
])->matching('Contracts', function ($q) {
    return $q->where(['Contracts.end_date is null'])
            ->orWhere(['Contracts.end_date >' => date('Y-m-d')]);
});
```

Estos ejemplos muestran diferentes formas de realizar consultas complejas en CakePHP, desde consultas con condiciones anidadas hasta consultas SQL directas y consultas con funciones de agregación.