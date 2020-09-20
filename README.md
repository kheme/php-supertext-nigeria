<h2 align="center">
    PHP Wrapper for [SuperText Nigeria](https://www.supertextng.com) SMS Gateway
</h2>

<p align="center">
    <a href="https://packagist.org/packages/kheme/php-supertext-nigeria">
        <img src="https://poser.pugx.org/kheme/php-supertext-nigeria/v/stable" alt="Latest Stable Version">
    </a>
    <a href="https://packagist.org/packages/kheme/php-supertext-nigeria">
        <img src="https://poser.pugx.org/kheme/php-supertext-nigeria/v/unstable" alt="Latest Unstable Version">
    </a>
    <a href="https://packagist.org/packages/kheme/php-supertext-nigeria">
        <img src="https://poser.pugx.org/kheme/php-supertext-nigeria/downloads" alt="Total Downloads">
    </a>
    <a href="https://packagist.org/packages/kheme/php-supertext-nigeria">
        <img src="https://poser.pugx.org/kheme/php-supertext-nigeria/license" alt="License">
    </a>
</p>

## Introduction

This is a simple PHP wrapper for [SuperText Nigeria](https://www.supertextng.com/)'s SMS API gateway.

## Installation

Using Composer:

```bash
composer require kheme/php-supertext-nigeria
```

### Usage
Import the class before making your calls.
```php
require_once 'vendor/autoload.php';
use Kheme\SuperTextNg\SMS;
```

Sending to a single recipient
-----------------------------

```php
$sms = new SMS('SUPERTEXTNG_USERNAME', 'SUPERTEXTNG_PASSWORD');
$sms->from('Kheme');
$sms->to('2348153332428')
$sms->message('Using the facade to send a message.')
$sms->send();   // returns true
```

If sending wasn't successful, an exception will be thrown.

Sending to multiple recipients
------------------------------

You can send an SMS to multiple recipients by including multiple `to()` in your call:

```php
$sms = new SMS('SUPERTEXTNG_USERNAME', 'SUPERTEXTNG_PASSWORD');
$sms->from('Kheme');
$sms->to('2348153332428');
$sms->to('2348056511193');
$sms->message('Using the facade to send a message.');
$sms->send();   // returns true
```

Or, by supplying an array of phone numbers to a single `to()`:

```php
$sms = new SMS('SUPERTEXTNG_USERNAME', 'SUPERTEXTNG_PASSWORD');
$sms->from('Kheme');
$sms->to([
    '2348153332428',
    '2348056512393',
]);
$sms->message('Using the facade to send a message.');
$sms->send();   // returns true
```

Send to DND enabled numbers
------------------------

To send SMS to numbers that have Do Not Disturb (DND) enabled, include `ignoreDND()` to your call:

```php
$sms = new SMS('SUPERTEXTNG_USERNAME', 'SUPERTEXTNG_PASSWORD');
$sms->from('Kheme');
$sms->to('2348153332428');
$sms->message('Using the facade to send a message.');
$sms->ignoreDND();
$sms->send();   // returns true
```

Return unit balance after sending
------------------------

If you would like to return your account balance after sending, include `returnBalance()` to your call:

```php
$sms = new SMS('SUPERTEXTNG_USERNAME', 'SUPERTEXTNG_PASSWORD');
$sms->from('Kheme');
$sms->to('2348153332428');
$sms->message('Using the facade to send a message.');
$sms->returnBalance();
$sms->send();   // returns true
```

Return amount of units used for sending
------------------------

If you would like to return the total amount of units used after sending, include `returnUnitsUsed()` to your call:

```php
$sms = new SMS('SUPERTEXTNG_USERNAME', 'SUPERTEXTNG_PASSWORD');
$sms->from('Kheme');
$sms->to('2348153332428');
$sms->message('Using the facade to send a message.');
$sms->returnUnitsUsed();
$sms->send();   // returns true
```

Combining options
------------------------

The above method options, exluding the `balance()` below, can be combined like in the following example:

```php
$sms = new SMS('SUPERTEXTNG_USERNAME', 'SUPERTEXTNG_PASSWORD');
$sms->from('Kheme');;
$sms->to('2348153332428');
$sms->message('Using the facade to send a message.');
$sms->returnBalance();
$sms->returnUnitsUsed();
$sms->ignoreDND();
$sms->send();   // returns true
```

Checking account balance
------------------------

To check your SuperText Nigeria credit balance, simply call `balance()`:

```php
$sms = new SMS('SUPERTEXTNG_USERNAME', 'SUPERTEXTNG_PASSWORD');
return $sms->balance();
```

### Errors

In the case of an error, a call will return an error as follows:

*The numbers on the left are the corresponding error code from SuperText Nigeria, but will not be included in the error response*

- **100**: *One or more required url parameter is missing or misspelt*
- **101**: *Username is blank*
- **102**: *Password is blank*
- **103**: *Destination is blank*
- **104**: *Message is blank*
- **105**: *Sender is blank*
- **200**: *Wrong username or password*
- **201**: *Account has not been activated*
- **202**: *Inactive account*
- **300**: *Insufficient credit*
- **400**: *Failed delivery (no credit deducted)*
