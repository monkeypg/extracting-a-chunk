# extracting-a-chunk-from-a-string

## 要取出$shifts中的A7/B9....

## 寫法一
```php
<?php

require_once 'vendor/autoload.php';

$shifts = [
    'Shipping_Steve_A7',
    'Sales_B9',
    'Support_Tara_K11',
    'J15',
    'Warehouse_B2',
    'Shipping_Dave_A6',
];

//如果要把$shifts array中_A7/B9...取出來，傳統PHP的方式是這樣做的
$shiftIds = collect($shifts)->map(function ($shift) {
    if (strrpos($shift, '_') !== false) {
        $underscorePosition = strrpos($shift, '_');
        $substringOffset = $underscorePosition + 1;
        return substr($shift, $substringOffset);
    } else {
        return $shift;
    }
});

var_dump($shiftIds->all()); exit;
$shiftIds = [
    'A7',
    'B9',
    'K11',
    'J15',
    'B2',
    'A6',
];
```

## 寫法二
```php
<?php

require_once 'vendor/autoload.php';

$shifts = [
    'Shipping_Steve_A7',
    'Sales_B9',
    'Support_Tara_K11',
    'J15',
    'Warehouse_B2',
    'Shipping_Dave_A6',
];

$shiftIds = collect($shifts)->map(function ($shift) {
    return collect(explode('_', $shift))->last();
});

var_dump($shiftIds->all()); exit;

$shiftIds = [
    'A7',
    'B9',
    'K11',
    'J15',
    'B2',
    'A6',
];
```