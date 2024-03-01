Class Cake\ORM\Table | CakePHP 3.1l

```
$workers = $this->Workers->find('all', [
    'conditions' => [
        'Workers.id IN' => $this->Contracts->find('all', [
            'conditions' => ['OR' => ['category_ciqus_id IN' => $conditions]],
        ])->select('worker_id')->where(['end_date is null', 'category_ciqus_id IN' => $conditions])->orWhere(['end_date >' => date('Y-m-d'), 'category_ciqus_id IN' => $conditions])
            
    ]
]);
$passesUsers = $this->PassesUsers->find('all', [
  'conditions' => [
    'vehicle_id' => $vehicle->id,
    'PassesUsers.start_date >=' => date('Y-m-d'),
    'PassesUsers.end_date <=' => date('Y-m-d'),
    'payed' => true,
    'temp' => false,
    'PassesUsers.pass_id IN' => $this->Passes->find('all', [
      'conditions' => [
        'Passes.id IN' => $this->PassesParkings->find('all', [
          'conditions' => [
            'parking_id IN' => $this->UsersParkings->find('all', [
              'conditions' => [
                'user_id' => $id
              ],
            ])->select('UsersParkings.parking_id')
          ],
        ])->select('PassesParkings.pass_id')
      ],
    ])->select('Passes.id')
  ],
  'contain' => ['Creator', 'Driver', 'Vehicles', 'Passes' => ['VehiclesTypes', 'PassesParkings' => 'Parkings']]
])->first();
```

```
$workers = $this->Workers->find('all', [
    'conditions' => [
        'Workers.id IN' => $this->Contracts->find('all')->select('worker_id')->where(['end_date is null', 'category_ciqus_id IN' => $categories_ids])->orWhere(['end_date >' => date('Y-m-d'), 'category_ciqus_id IN' => $categories_ids])
    ]
]);
```

```
SELECT name, date from mod_calendars where idUser_fk=3 and MONTH(CURRENT_DATE()) < MONTH(date);
SELECT name, date from mod_calendars where idUser_fk=3 and MONTH(CURRENT_DATE())+1 = MONTH(date);
```
Retrieving Your Data - 2.x

SUM/AVG/COUNT

```
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

```
 $total_rentals_payments = $rentals_payments_all->select(['sum' => $rentals_payments_all->func()->sum('PaymentsToAccounts.amount')])->where(['DATE(PaymentsToAccounts.date) >=' => $start_date, 'DATE(PaymentsToAccounts.date) <=' => $end_date])->first()->toArray();
```

```
$passes_ids_orm = $this->PassesParkings->find('all', ['conditions' => ['parking_id' => $parking_id] ])->select(['pass_id'])->distinct(['pass_id']);

```
Consulta con SQL

```
use Cake\Datasource\ConnectionManager;
$connection = ConnectionManager::get('default');
                $total_earnings_tickets = $connection
                    ->execute(
                        'SELECT (SUM(total_tax)) AS "total_tax", (SUM(total_discounted)) AS "discount", (SUM(total_without_tax)) AS "total_without_tax", (SUM(total)) AS "total_calculated" FROM tickets WHERE (parking_id = ' . $parking->id . ' AND status = 1 AND date(output_date) >= \'' . date('Y-m-d', strtotime($firstDayOfMonth) ) . '\' AND date(output_date) < \'' . date('Y-m-d', strtotime($lastDayOfMonth) ) . '\'::date)'
                    )
                    ->fetchAll('assoc')[0];
```
Natural sort (para ordenar por orden alfabético) (ejecutar en el postgres, es una función)

```
create or replace function naturalsort(text)
returns bytea language sql immutable strict as $f$
select string_agg(convert_to(coalesce(r[2], length(length(r[1])::text) || length(r[1])::text || r[1]), 'SQL_ASCII'),'\x00')
from regexp_matches($1, '0*([0-9]+)|([^0-9]+)', 'g') r;
$f$;
```

```
$contracts_by_sexes = $this->Workers->find('all', [
                    'contain' => ['Sexes'],
                    'group' => 'Sexes.name',
                    'fields' => array(
                        "count_contracts_sex"=>"COUNT(Sexes.name)", 
                        'name' => 'Sexes.name'
                    )
                ])->matching('Contracts', function ($q) {
                    return $q->where(['Contracts.end_date is null'])
                           ->orWhere(['Contracts.end_date >' => date('Y-m-d')]);
                });
```