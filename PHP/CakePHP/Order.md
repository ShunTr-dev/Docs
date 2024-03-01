```


if($this->request->query['sort'] != null && $this->request->query['direction'] != null){
            $sort = $this->request->query['sort'];
            $direction = $this->request->query['direction'];
        } else {
            $sort = 'ResearchGroups_name_translation.content';
            $direction = 'ASC';
        }
```
Note that if you want to be able to sort by other fields than the one passed explicitly in a query object, you’ll need to mix the two methods:

```
$this->paginate['sortWhitelist'] = $this->Users->schema()->columns() + ['Cities.id', 'Cities.name'];
$query = $this->Users->find()
                     ->contain('Cities')
                     ->order(['Cities.name' => 'DESC']);
$users = $this->paginate($query);
```

```
if(isset($this->request->query['sort']) && isset($this->request->query['direction'])){
            $sort = $this->request->query['sort'];
            $direction = $this->request->query['direction'];
        } else {
            $sort = 'ResearchGroups_name_translation.content';
            $direction = 'ASC';
        }
        if(empty($type)){
            $type = 'active';
            $researchGroups = $this->paginate(
                $this->ResearchGroups->find('all', [
                    'order' => [$sort => $direction],
                    'conditions' => [
                        'OR' => [
                            'end_date >' => date('Y-m-d'),
                            'end_date is null',
                        ]
                    ]
                ])
            );
        } else {
            $type = 'all';
            $researchGroups = $this->paginate(
                $this->ResearchGroups->find('all', [
                    'order' => [$sort => $direction]
                ])
            );
        }
```