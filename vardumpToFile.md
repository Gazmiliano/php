```php
ob_start();
echo date('Y-m-d H:i:s');
var_dump($var);
$data = ob_get_clean();
$fp = fopen('debug.log', 'a');
fwrite($fp, $data);
fclose($fp);
```
