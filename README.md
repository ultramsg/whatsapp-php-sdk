# [Ultramsg.com](https://ultramsg.com/?utm_source=github&utm_medium=php&utm_campaign=api) WhatsApp API PHP SDK

 Lightweight PHP library for WhatsApp API to send the whatsappp messages in PHP provided by [Ultramsg.com](https://ultramsg.com/?utm_source=github&utm_medium=php&utm_campaign=api)

# Installation

Just download ultramsg.class.php or use Composer: 

```
composer require ultramsg/whatsapp-php-sdk
```


# Example usage

```php
<?php
require_once ('vendor/autoload.php'); // if you use Composer
//require_once('ultramsg.class.php'); // if you download ultramsg.class.php

$ultramsg_token="tof7lsdJasdloaa57e"; // Ultramsg.com token
$instance_id="instance1150"; // Ultramsg.com instance id
$client = new UltraMsg\WhatsAppApi($ultramsg_token,$instance_id);

$to="put_your_mobile_number_here"; 
$body="Hello world"; 
$api=$client->sendChatMessage($to,$body);
print_r($api);
```
 > **NOTE:**  you need replace instance_id and token with yours in [ultramsg.com](https://ultramsg.com/?utm_source=github&utm_medium=php&utm_campaign=api) account if you don't have account create one from [here](https://ultramsg.com/?utm_source=github&utm_medium=php&utm_campaign=api)

# Youtube
[![Send Message by WhatsApp api using PHP SDK | Ultramsg PHP SDK
](https://img.youtube.com/vi/OqDOKyMIp20/0.jpg)](https://www.youtube.com/watch?v=OqDOKyMIp20)


## Send Message
* **$to** :  your number for testing with international format e.g. +14155552671 or chatID for contact or group e.g 14155552671@c.us or 14155552671-441234567890@g.us
* **$body** : Message text, UTF-8 or UTF-16 string with emoji .
* **$priority** : This parameter is optional,

You can use it to create a professional queue for messages, The Messages with less priority value are sent first.

example of usage :

priority = 0: for High priority like OTP messages.

priority = 5: used with general messages.

priority =10: Non-urgent promotional offers and notifications to your customers.

**Default value** : 10
* **$referenceId** : Your custom reference ID for this message.
```php
$to="put_your_mobile_number_here"; 
$body="Hello world";
$priority=10;
$referenceId="SDK";
$api=$client->sendChatMessage($to,$body,$priority,$referenceId);
print_r($api);
```

## Send Image 
* **$caption** : image Caption, UTF-8 or UTF-16 string with emoji .
* **$image** : HTTP link image or base64-encoded file

Supported extensions ( jpg , jpeg , gif , png , svg , webp , bmp ) .

Max file size : 16MB .

Max Base64 length : 2,000,000

* **$nocache** : default false

false : use a previously uploaded file instead of uploading it with each request

true : uploading it each request

```php
$to="put_your_mobile_number_here"; 
$image="https://file-example.s3-accelerate.amazonaws.com/images/test.jpg"; 
$caption="image Caption"; 
$priority=10;
$referenceId="SDK"
$nocache=false; 
$api=$client->sendImageMessage($to,$image,$caption,$priority,$referenceId,$nocache);
print_r($api);
```
## Send Document 
* **$filename** : File name, for example 1.jpg or Hello.pdf
* **$document** : HTTP link file or base64-encoded file

Supported most extensions like ( zip , xlsx , csv , txt , pptx , docx ....etc ) .

Max file size : 100MB .

Max Base64 length : 2,000,000

```php
$to="put_your_mobile_number_here"; 
$filename="image Caption"; 
$document="https://file-example.s3-accelerate.amazonaws.com/documents/cv.pdf"; 
$api=$client->sendDocumentMessage($to,$filename,$document);
print_r($api);
```

## Send Audio 
* **$audio** : HTTP link audio or base64-encoded audio 

Supported extensions ( mp3 , aac , ogg ) .

Max file size : 16MB .

Max Base64 length : 2,000,000

```php 
$to="put_your_mobile_number_here"; 
$audio="https://file-example.s3-accelerate.amazonaws.com/audio/2.mp3"; 
$api=$client->sendAudioMessage($to,$audio);
print_r($api);
```
## Send Voice 
* **$audio** : HTTP link audio ogg-file with opus codec or base64 ogg-file in opus codec

Max file size : 16MB .

Max Base64 length : 2,000,000

```php 
$to="put_your_mobile_number_here"; 
$audio="https://file-example.s3-accelerate.amazonaws.com/voice/oog_example.ogg"; 
$api=$client->sendVoiceMessage($to,$audio);
print_r($api);
```

## Send Video 
* **$video** : HTTP link video or base64-encoded video  

Supported extensions ( mp4 , 3gp , mov ) .

Max file size : 16MB .

Max Base64 length : 2,000,000

```php 
$to="put_your_mobile_number_here"; 
$video="https://file-example.s3-accelerate.amazonaws.com/video/test.mp4";
$caption="video Caption"; 
$api=$client->sendVideoMessage($to,$video,$caption);
print_r($api);
```
## Send Link 
* **$link** : HTTP or HTTPS link

```php 
$to="put_your_mobile_number_here"; 
$link="https://ultramsg.com"; 
$api=$client->sendLinkMessage($to,$link);
print_r($api);
```
## Send Contact 
* **$contact** :Contact ID or Contact IDs array example :

Example

14000000001@c.us

or

14000000001@c.us,14000000002@c.us,14000000003@c.us

Max length : 300 char, almost 15 contacts
```php 
$to="put_your_mobile_number_here"; 
$contact="14000000001@c.us"; 
$api=$client->sendContactMessage($to,$contact);
print_r($api);
```
## Send Location 
* **$address** : Text under the location.

Supports two lines. To use two lines, use the \n symbol.

Max length : 300 char .
* **$lat** : Latitude
* **$lng** : longitude
```php 
$to="put_your_mobile_number_here"; 
$address="ABC company \n Sixth floor , office 38"; 
$lat="25.197197"; 
$lng="55.2721877"; 
$api=$client->sendLocationMessage($to,$address,$lat,$lng);
print_r($api);
```
## Send Vcard 
* **$vcard** : Text value vcard 3.0

Max length : 4096 char

```php 
$to="put_your_mobile_number_here"; 
$vcard="BEGIN:VCARD
VERSION:3.0
N:lastname;firstname
FN:firstname lastname
TEL;TYPE=CELL;waid=14000000001:14000000002
NICKNAME:nickname
BDAY:01.01.1987
X-GENDER:M
NOTE:note
ADR;TYPE=home
ADR;TYPE=work
END:VCARD";
$vcard = preg_replace("/[\n\r]/", "\n", $vcard);
$api=$client->sendVcardMessage($to,$vcard);
print_r($api);
```

## Resend messages by status 
* **$status** :  unsent or expired
 
```php 
$status="expired";
$api=$client->resendByStatus($status);
print_r($api);
```

## Resend message by ID 
* **$id** :   message id
 
```php
$id=123;
$api=$client->resendById($id);
print_r($api);
```

## Get Messages
get the messages that sent by api

* **$page** : pagination page number
* **$limit** : number of messages per request . max value : 100 .
* **$status** : Messages status [sent , queue , unsent]
  - sent : get sent messages .
  - queue : get queue messages .
  - unsent : get unsent messages .
  - invalid : get invalid messages .
  - expired : get expired messages .
  - all : get all messages .
* **$sort** :  
  - asc : sorted messages by ID from smallest to largest .
  - desc : sorted messages by ID from largest to smallest .
* **$id** : filter messages by message ID .
* **$referenceId** : filter messages by your custom reference ID .
* **$from** : filter messages by WhatsApp sender number e.g 14155552671@c.us .
* **$to** : filter messages by recipient number  e.g 14155552671@c.us or 14155552671-441234567890@g.us .
* **$ack** : filter messages by message ack status [ pending , server , device , read , played ] .


```php 
$page=1;
$limit=100;
$status="all";
$sort="asc";
$id="";
$referenceId="";
$from="";
$to="";
$ack="";
$api=$client->getMessages($page,$limit,$status,$sort,$id,$referenceId,$from,$to,$ack);
print_r($api);
```

## Get Messages Statistics 

```php 
$api=$client->getMessageStatistics();
print_r($api);
```

## Get Instance Status 

```php 
$api=$client->getInstanceStatus();
print_r($api);
```

## Get Instance QR Image

```php 
header('Content-Type: image/png');
$api=$client->getInstanceQr();
print_r($api);
```
## Get Instance QR Code 

```php  
$api=$client->getInstanceQrCode();
print_r($api);
```
## Get Instance Screenshot 
 
```php  
header('Content-Type: image/png');
$api=$client->getInstanceScreenshot();
print_r($api);
```
or base64
```php
$api=$client->getInstanceScreenshot("base64");
print_r($api);
```
## Get Instance Info
Get connected phone informations : number , name , image etc..
```php
$api=$client->getInstanceMe();
print_r($api);
```
## Get Instance Settings
sendDelay : Delay in seconds between sending message, Default 1 second

webhook_url : Http or https URL for receiving notifications .

webhook_message_ack : on/off ack (message delivered and message viewed) notifications in webhooks.

webhook_message_received : on/off notifications in webhooks when message received .

webhook_message_create : on/off notifications in webhooks when message create .

webhook_message_download_media  :  on/off to get received document / media files.
```php
$api=$client->getInstanceSettings();
print_r($api);
```

## Instance Takeover
Returns the active session if the device has connected to another instance of Web WhatsApp

```php  
$api=$client->sendInstanceTakeover();
print_r($api);
```
## Instance Logout
Logout from WhatsApp Web to get new QR code.

```php  
$api=$client->sendInstanceLogout();
print_r($api);
```
## Instance Restart
Restart your instance.

```php  
$api=$client->sendInstanceRestart();
print_r($api);
```
## Instance Settings Update
* **sendDelay** : Delay in seconds between sending message .

* **webhook_url** : Http or https URL for receiving notifications .

* **webhook_message_received** : true/false notifications in webhooks when message received .

* **webhook_message_create** : true/false notifications in webhooks when message create .

* **webhook_message_ack** : true/false ack (message delivered and message viewed) notifications in webhooks.

```php  
$sendDelay=1;
$webhook_url="";
$webhook_message_received=false;
$webhook_message_create=false;
$webhook_message_ack=false;
$webhook_message_download_media=false;

$api=$client->sendInstanceSettings($sendDelay,$webhook_url,$webhook_message_received,$webhook_message_create,$webhook_message_ack,$webhook_message_download_media);
print_r($api);
```

## Get the chats list

```php  
$api=$client->getChats();
print_r($api);
```

## get last message from chat conversation

* **$chatId** : chatID for contact or group e.g 14155552671@c.us or 14155552671-441234567890@g.us
* **$limit** : number of messages per request .

max value : 1000 .

```php  
$chatId="14155552671@c.us";
$limit=100;
$api=$client->getChatsMessages($chatId,$limit);
print_r($api);
```


## Get the contacts list

```php  
$api=$client->getContacts();
print_r($api);
```

## Get contact info

* **$chatId** : chatID for contact e.g 14155552671@c.us 

```php  
$chatId="14155552671@c.us"; 
$api=$client->getContact($chatId);
print_r($api);
```


## Gets all blocked contacts

```php  
$api=$client->getBlockedContacts();
print_r($api);
```

## block contact from WhatsApp

* **$chatId** : chatID for contact e.g 14155552671@c.us 

```php  
$chatId="14155552671@c.us"; 
$api=$client->blockContact($chatId);
print_r($api);
```

## Unblock contact from WhatsApp

* **$chatId** : chatID for contact e.g 14155552671@c.us 

```php  
$chatId="14155552671@c.us"; 
$api=$client->unblockContact($chatId);
print_r($api);
```

## Check if number is WhatsApp user

* **$chatId** : chatID for contact e.g 14155552671@c.us 

```php  
$chatId="14155552671@c.us"; 
$api=$client->checkContact($chatId);
print_r($api);
```



# Support
Use **Issues** to contact me