<!--
  Title: FIFA 18 WebApp API
  Description: A simply way to manage your FIFA 18 Ultimate Team with a PHP framework..
  Author: Curtis Crewe
  -->

FIFA 18 WebApp API
=============

Manage your FIFA 18 Ultimate Team using this FIFA 18 Ultimate Team API.
Written solely in PHP

Installing FUTApi
=======

The recommended way to install FIFA 18 WebApp API is through
[Composer](http://getcomposer.org).

```bash
# Install Composer
curl -sS https://getcomposer.org/installer | php
```

Next, run the Composer command to install the latest stable version of Guzzle:

```bash
composer require inkedcurtis/fut-api=dev-master
```

After installing, you need to require Composer's autoloader:

```php
require 'vendor/autoload.php';
```

Documentation
=============

Players database: https://www.easports.com/uk/fifa/ultimate-team/fut/database

Players database (json): https://www.easports.com/fifa/ultimate-team/web-app/content/B1BA185F-AD7C-4128-8A64-746DE4EC5A82/2018/fut/items/web/players_meta.json

Python source provided by: https://github.com/futapi/fut/

Contact
=======

Skype: bws-curtis<br/>
Email: admin@curtiscrewe.co.uk

Usage
=====

Login
-----

Optional parameters:

- code: [string] email/sms code for two-step verification (make sure to use string if your code starts with 0).
- platform: [pc/ps3/ps4/xbox/xbox360].
- emualte: [and/ios] currently DISABLED.
- cookies: [filename] path to cookies file, if not provided it'll be created in a 'cookies' directory.

```php
use FUTApi\Core;
use FUTApi\FutError;
try {
    $fut = new Core('email', 'password', 'secret answer', 'platform', 'backup_code');
} catch(FutError $e) {
    $error = $e->GetOptions();
    die("We have an error logging in: ".$error['reason']);
}
$login = $fut->login();
```

After you have initiated your first session, you can then use the API wthout logging in again using the session info from your original login array:

```php
use FUTApi\Core;
use FUTApi\FutError;
$fut = new Core('email', 'password', 'secret answer', 'platform', 'backup_code');
$fut->setSession($persona, $nucleus, $phishing, $session, $dob);
```

    
Search
------

Optional parameters:

- min_price: [int] Minimal price.
- max_price: [int] Maximum price.
- min_buy: [int] Minimal buy now price.
- max_buy: [int] Maximum buy now price.
- level: ['bronze'/'silver'/gold'] Card level.
- start: [int] Start page number.
- category: ['fitness'/'?'] Card category.
- assetId: [int] assetId.
- defId: [int] defId.
- league: [int] League id.
- club: [int] Club id.
- position: [int?/str?] Position.
- zone: ['attacker'/'?'] zone.
- nationality: [int] Nation id.
- rare: [boolean] True for searching special cards.
- playStyle: [str?] playStyle.
- page_size: [int] Amount of cards on single page (changing this might be risky).

```php
$items = $fut->searchAuctions('player');
```
    
Logout
------

Replicates clicking the Logout button.

    $fut->logout();


License
-------

GNU GPLv3
