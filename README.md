# Laravel - Twilio

>##WHAT IT IS?

- This package is used to send sms to any mobile number.
- This uses [Twilio](https://www.twilio.com/) API.
- It requires *AccountSID* and *AuthToken*, they can be generated by registrting @at [Twilio](https://www.twilio.com/try-twilio)
  - after registration click on Account ,there you will be able to see authsid and authtoken. 
  - You have assigned a sender mobile number which can be found at [Twilio](https://www.twilio.com/user/account/phone-numbers/incoming),which is used to send Text Messages or MMS and ShortCodes etc.

***

>##INSTALLATION

 - Download package form  https://github.com/lakshmajim/twilio . 
 - OR YOU CAN RUN FOLLOWING COMMAND FROM TERMINAL
 - With composer you can run this line **composer require lakshmajim/twilio**

Run this command from the Terminal:

```bash
    composer require lakshmajim/twilio
    composer dumpautoload
    composer update
```

***

>##Laravel INTEGRATION

you need to add the service provider. Open `app/config/app.php`, and add a new item to the providers array.
```php
  Lakshmajim\Twilio\TwilioServiceProvider::class,
```
Then, add a Facade for more convenient usage. In `app/config/app.php` add the following line to the `aliases` array:
```php
  'Twilio'    => Lakshmajim\Twilio\Facade\Twilio::class,
```
Again do composer update

***

#METHOD 1:
>###Sending SMS

```php

<?php
use Twilio;
Twilio::sendMessageTwilio($auth_id,$auth_token);

```

>###Miscellaneous

```php

<?php
  Use Twilio;
  //setting source mobile number
  Twilio::setSourceMobile("918888888888");
  //setting destination mobile number
  Twilio::setDestinationMobile("919999999999");
  //setting text message
  Twilio::setMessageTwilio("Your text message or otp here");
  
```


>###Example code for Laravel

```php

<?php namespace App\Http\Controllers;

use Illuminate\Routing\Controller as BaseController;
use Twilio;

class TwilioClass extends Controller
{
  public function sendSMS()
  {
    $src       = Twilio::setSourceMobile("+XXXXXXXXXX");
    $dest      = Twilio::setDestinationMobile("+XXXXXXXXXX");
    $txt       = Twilio::setMessageTwilio("lakshmaji - Testing from package");
    $smsObject = Twilio::sendMessageTwilio('<AUTH_SID>','AUTH_TOKEN');
    echo $smsObject;         //diaplay final message response
  }
}

```

***



#METHOD 2:
>###Manage Twilio creadential at one safe place 
Keep Twilio credentials in Laravel .env file as follows

```php

TWILIO_AUTH_ID=<YOUR_AUTH_SID_FROM_TWILIO>
TWILIO_AUTH_SECRET=<YOUR_AUTH_TOKEN_FROM_TWILIO>
TWILIO_SOURCE_NUMBER=+<YOUR_SENDER_MOBILE_NUMBER_FROM_TWILIO>


```
Just use the follwing single line to make your message deliverable.
```php

  Twilio::sendSMS(<ARRAY_DATA>,<YOUR_MESSAGE_TEXT>,<MESSAGE_TYPE>);


```
PARAMETERS

| PARAMETER           | DESCRIPTION                             |
|:------------------- |:----------------------------------------| 
| YOUR_MESSAGE_TEXT   | Message text to be send                 | 
|  MESSAGE_TYPE       | Message type (OTP,SMS)                  |
|  ARRAY_DATA         | Consists of 'mobile_number' and 'otp'   |

NOTE :
```php

    default <MESSAGE_TYPE> is "SMS"
    'otp' index in <ARRAY_DATA> is optional 
    defining array_data as follows.
    $your_array_name = array( 'mobile_number'=> <Your _destination_mobile_number>,'otp'=><your_code>);


```

>###Example Usage

##Sending OTP

```php

<?php

use Twilio;
class SendSmsTwilio extends Controller
{
  $userMobileData = array(
                           'mobile_number' => <YOUR_MOBILE_NUMBER_HERE>,
                           'otp'           => <YOUR_OTP_HERE>,
                          );       
  if(Twilio::sendSMS($userMobileData,"OTP to verify mobile number","OTP")) 
  {
    echo "sms sent successfully";
  }
  else
  {
    echo "sms delivery failed";
  }
}

```
##Sending Message

```php

<?php

use Twilio;
class SendSmsTwilio extends Controller
{
  $userMobileData = array(
                           'mobile_number' => <YOUR_MOBILE_NUMBER_HERE>
                         );       
  if(Twilio::sendSMS($userMobileData,"This is only textual message")) 
  {
    echo "sms sent successfully";
  }
  else
  {
    echo "sms delivery failed";
  }
}

```

*** 
***




>## TWILIO TRAIL ACCOUNT USAGE:

 - If You are trying to implement SMS functionality with Twilio the you need to verify the list of destination mobile numbers at [Twilio](https://www.twilio.com/user/account/phone-numbers/verified)
![VERIFIED NUMBERS](https://raw.githubusercontent.com/lakshmajim/images/master/verified_numbers.png)
 - Before sending MESSAGE make sure that you have enabled **GEO-PERMISSIONS** at [Twilio](https://www.twilio.com/user/account/settings/international)
![GEO PERMISSIONS](https://raw.githubusercontent.com/lakshmajim/images/master/geo_permissions.png)

***

>##Licence

[*MIT License (MIT)*](https://opensource.org/licenses/MIT)

@ MUTYALA ANANTHA LAKSHMAJI
