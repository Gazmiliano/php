```php
// Array to send
$request = [];

// Endpoint 
$url = 'https://example.com';

// Init curl
$ch = curl_init();

// Curl options
curl_setopt($ch, CURLOPT_URL, $url);
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
curl_setopt($ch, CURLOPT_SSL_VERIFYPEER, false);
curl_setopt($ch, CURLOPT_POST, 1);
curl_setopt($ch, CURLOPT_POSTFIELDS, http_build_query($request));
$response = curl_exec($ch);
curl_close($ch);

// View result
echo $response;
```
