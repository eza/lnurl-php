# lnurl-php
This is a PHP implementation of the `lnurl` protocol https://github.com/fiatjaf/lnurl-rfc

This repo is a fork of: https://github.com/tkijewski/php-lnurl.
I have improved the code, added testing and PHP8 support, 
and more importantly I added support for `lnurl-auth` (https://github.com/fiatjaf/lnurl-rfc/blob/luds/04.md).

## Installation

```
$ composer require eza/lnurl-php
```


## Usage
I have also written an article on how you could potentially implement this in your own PHP application here [https://zadrima.com/lnurl-auth-in-php/](https://zadrima.com/lnurl-auth-in-php/)

```
<?php

require __DIR__ . '/vendor/autoload.php';

use eza\lnurl;

// Encode a URL to LNURL
$lnurl = lnurl\encodeUrl('https://paywall.link?someIdentifier=292e29j29j19nd91m2mfmmurn843&tag=withdraw');
//LNURL1DP68GURN8GHJ7URP09MKZMRV9EKXJMNT8AEK7MT9F9JX2MN5D9NXJETJ85ERJVN9XGUK5V3EDGCNJMNY8YCK6VNDVEKK6ATJDCURGVEXW3SKW0THD96XSERJV9MS95LDUW

// Decode from LNURL
print_r( lnurl\decodeUrl($lnurl) );
/*
 * [
 *   'url' => 'https://paywall.link?someIdentifier=292e29j29j19nd91m2mfmmurn843&tag=withdraw',
 *   'tag' => 'withdraw'
 *   'someIdentifier' => '292e29j29j19nd91m2mfmmurn843'
 * ] 
 */
 
// LNURL Auth
if (lnurl\auth($request->k1, $request->signature, $request->wallet_public_key)) {
    // fetch or create user then authenticate
}

```

## Test

```
$ vendor/bin/phpunit
```
