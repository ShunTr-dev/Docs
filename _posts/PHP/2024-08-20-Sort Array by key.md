---
title: Sort Array by key
date: 2024-08-20 00:00:00 -100
categories: [PHP]
tags: [php, ordenacion]
---

# Ordenar un array por clave

El siguiente código en PHP proporciona una función `array_sort` que ordena un array asociativo por una clave específica, manteniendo la asociación de índices. Aquí está el código:

```php
<?php

function array_sort($array, $on, $order=SORT_ASC)
{
    $new_array = array();
    $sortable_array = array();

    if (count($array) > 0) {
        foreach ($array as $k => $v) {
            if (is_array($v)) {
                foreach ($v as $k2 => $v2) {
                    if ($k2 == $on) {
                        $sortable_array[$k] = $v2;
                    }
                }
            } else {
                $sortable_array[$k] = $v;
            }
        }

        switch ($order) {
            case SORT_ASC:
                asort($sortable_array);
            break;
            case SORT_DESC:
                arsort($sortable_array);
            break;
        }

        foreach ($sortable_array as $k => $v) {
            $new_array[$k] = $array[$k];
        }
    }

    return $new_array;
}

$people = array(
    12345 => array(
        'id' => 12345,
        'first_name' => 'Joe',
        'surname' => 'Bloggs',
        'age' => 23,
        'sex' => 'm'
    ),
    12346 => array(
        'id' => 12346,
        'first_name' => 'Adam',
        'surname' => 'Smith',
        'age' => 18,
        'sex' => 'm'
    ),
    12347 => array(
        'id' => 12347,
        'first_name' => 'Amy',
        'surname' => 'Jones',
        'age' => 21,
        'sex' => 'f'
    )
);

print_r(array_sort($people, 'age', SORT_DESC)); // Ordena por edad de mayor a menor
print_r(array_sort($people, 'surname', SORT_ASC)); // Ordena por apellido de forma ascendente

?>
```
