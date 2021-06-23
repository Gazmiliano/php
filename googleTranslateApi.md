### Url
https://github.com/aalfiann/google-translate-api-php

- If you are not specify the source of language, then Google will detect it automatically.
- You should cache the results, because Google has LIMIT RATE and will block your IP address server if too many request.

### Composer.json
```json
{
    "require": {
        "aalfiann/google-translate-api-php": "^1.0"
    }
}
```

### Translate.php
```php
<?php

// =========================================================================
// Global
// =========================================================================

define('THIS_HOST', 'localhost');
define('THIS_USER', 'user');
define('THIS_PASS', 'password');
define('THIS_DB', 'database');

// =========================================================================
// Library
// =========================================================================

require_once ('vendor/autoload.php');
use \aalfiann\GoogleTranslate;

// =========================================================================
// Functions
// =========================================================================

function pdoConstSelect($sql)
{
    $host = THIS_HOST;
    $user = THIS_USER;
    $pass = THIS_PASS;
    $db = THIS_DB;

    $DBH = new PDO("mysql:host=$host;dbname=$db;charset=utf8", $user, $pass);
    $DBH->setAttribute(PDO::ATTR_ERRMODE, PDO::ERRMODE_WARNING);

    if (strpos($sql, 'SELECT ') !== false) {
        $result = $DBH->query($sql);
        if ($result !== FALSE) {
            $result = $result->fetchAll();
            $max = count($result);

            for($i = 0; $i < $max; ++$i) {
                foreach ($result[$i] as $a => $b) {
                    if (is_int($a)) {
                        unset($result[$i][$a]);
                    }
                }
            }
        }
        $is_error = $DBH->errorInfo();
        if ($is_error[0] !== '00000') {
            error_log($sql, 0);
            var_dump($is_error);
        }
        $DBH = null;
        return ($result);
    } else {
        $DBH->query($sql);

        $is_error = $DBH->errorInfo();
        if ($is_error[0] !== '00000') {
            error_log($sql, 0);
        }
        $DBH = null;
    }
}

// =========================================================================
// Translate
// =========================================================================

$sql = "SELECT id, ru_text FROM table WHERE en_text = '' LIMIT 200";
$result = pdoConstSelect($sql);

for ($i = 0, $iMax = count($result); $i < $iMax; $i++) {
    $lang = new GoogleTranslate();
    $lang->source = 'ru';
    $lang->target = 'en';
    $lang->text = $result[$i]['name_ru'];
    $tr = $lang->translate()->getText();

    if ($tr !== '') {
        $tr = str_replace("'s" , "", $tr);
        $tr = str_replace("'" , "", $tr);

        $sql = "UPDATE table SET en_text = '$tr' WHERE id = '". $result[$i]['id'] ."'";
        pdoConstSelect($sql);
    } else {
        break;
    }
}


```
