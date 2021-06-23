```php
#!/usr/bin/php -q
<?php
error_reporting(E_ALL);
require('phpagi.php'); 
$agi = new AGI();

//FCM API end-point
$url = 'https://fcm.googleapis.com/fcm/send';
$headers = array(
    'Content-Type:application/json',
    'Authorization:key=KEY'
);
		
$push_data =
    [
        'to' => "FCM_KEY",
        'data' => [
            'body' => [
				      'order_type' => 'question',
				      'message_type' => 'chat',
				      'message_id' => '592',
				      'order_id' => '9999',
				      'sender_id' => '16'
			      ]
        ]
    ];
$push_data = json_encode($push_data);

//CURL request to route notification to FCM connection server (provided by Google)

$ch = curl_init();
curl_setopt($ch, CURLOPT_URL, $url);
curl_setopt($ch, CURLOPT_POST, true);
curl_setopt($ch, CURLOPT_HTTPHEADER, $headers);
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
curl_setopt($ch, CURLOPT_SSL_VERIFYHOST, 0);
curl_setopt($ch, CURLOPT_SSL_VERIFYPEER, false);
curl_setopt($ch, CURLOPT_POSTFIELDS, $push_data);
$result = curl_exec($ch);

if ($result === FALSE) {
  echo curl_error($ch);
}	
curl_close($ch);

// EXAMPLE 1
set_time_limit(30);
require('include/phpagi.php');
require('phpagi.php');
error_reporting(E_ALL);

$agi = new AGI();
$agi->answer();
$agi->stream_file("demo-congrats","#");

do
{
	$agi->stream_file("enter-some-digits","#");
	$result = $agi->get_data('beep', 3000, 20);
	$keys = $result['result'];
	$agi->stream_file("you-entered","#");
	$agi->say_digits($keys);
} while($keys != '111');
	$agi->hangup();

// EXAMPLE 2
  set_time_limit(0);
  require('phpagi.php');

  $agi = new AGI();
  $cid = $agi->request['agi_callerid'];  // Caller ID
  
  $agi->text2wav("goodbye");
  $agi->hangup();
  
  if ($cid==8312222222) {                                    
  $agi->text2wav("Hi, Test message");
  $agi->hangup();
  }
?>
```  
