**Note: Moved to composer and namespaces! Read installation instructions and examples before updating, not backwards compatible with older beta client!**

Installation
------------------

Requires:
- [composer](http://getcomposer.org/)

Create or add the following to composer.json in your project root:
```javascript
{
    "repositories": [
        {
            "type": "vcs",
            "url": "https://github.com/EasyPost/easypost-php-beta"
        }
    ],
    "require": {
        "easypost/easypost-php": "master"
    }
}
```

Install composer dependancies:
```shell
php composer.phar install
```

Require dependancies:
```php
require_once("/path/to/vendor/autoload.php");
```

Example
----------------
```php
require_once("path/to/vendor/autoload.php");
\EasyPost\EasyPost::setApiKey('cueqNZUb3ldeWTNX7MU3Mel8UXtaAMUi');

$to_address = \EasyPost\Address::create(
    array(
        "street1" => "388 Townsend St",
        "street2" => "Apt 20",
        "city"    => "San Francisco",
        "state"   => "CA",
        "zip"     => "94107"
    )
);
$from_address = \EasyPost\Address::create(
    array(
        "company" => "Simpler Postage Inc",
        "street1" => "764 Warehouse Ave",
        "city"    => "Kansas City",
        "state"   => "KS",
        "zip"     => "66101",
        "phone"   => "620-123-4567"
    )
);
$parcel = \EasyPost\Parcel::create(
    array(
        "predefined_package" => "LargeFlatRateBox",
        "weight" => 76.9
    )
);
$shipment = \EasyPost\Shipment::create(
    array(
        "to_address"   => $to_address,
        "from_address" => $from_address,
        "parcel"       => $parcel
    )
);

$shipment->buy($shipment->lowest_rate());

echo $shipment->postage_label->label_url;
```

Documentation
--------------------

Up-to-date documentation at: https://www.geteasypost.com/docs/v2

Tests
--------------------
Install dev dependancies:
```shell
php composer.phar install --dev
```

Run tests:
```shell
path/to/bin/phpunit
```