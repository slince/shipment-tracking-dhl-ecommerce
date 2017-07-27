# Shipment Tracking Library For DHL eCommerce

[![Build Status](https://img.shields.io/travis/slince/shipment-tracking-dhlecommerce/master.svg?style=flat-square)](https://travis-ci.org/slince/shipment-tracking-dhlecommerce)
[![Coverage Status](https://img.shields.io/codecov/c/github/slince/shipment-tracking-dhlecommerce.svg?style=flat-square)](https://codecov.io/github/slince/shipment-tracking-dhlecommerce)
[![Latest Stable Version](https://img.shields.io/packagist/v/slince/shipment-tracking-dhlecommerce.svg?style=flat-square&label=stable)](https://packagist.org/packages/slince/shipment-tracking-dhlecommerce)
[![Scrutinizer](https://img.shields.io/scrutinizer/g/slince/shipment-tracking-dhlecommerce.svg?style=flat-square)](https://scrutinizer-ci.com/g/slince/shipment-tracking-dhlecommerce/?branch=master)

A flexible and shipment tracking library for DHL eCommerce or DHL eCommerce(Registered)

## Basic Usage


```php

$tracker = new Slince\ShipmentTracking\DHLECommerce\DHLECommerceTracker(CLIENT_ID, PASSWORD);

try {
   $shipment = $tracker->track('CNAQV100168101');
   
   if ($shipment->isDelivered()) {
       echo "Delivered";
   }
   echo $shipment->getOrigin();
   echo $shipment->getDestination();
   print_r($shipment->getEvents());  //print the shipment events
   
} catch (TrackException $exception) {
    exit('Track error: ' . $exception->getMessage());
}

```
The above code will get access token automatically for shipment information.

### Access Token

```php
$shipment = $tacker->track('CNAQV100168101);
$accessToken = $tracker->getAccessToken(); //You can save this for the next query

//... to do

try{
    $tracker->setAccessToken($accessToken); //Set the access token; the tracker will not send requst for the access token
    $shipment = $tacker->track('CNAQV100168101);
} catch (InvalidAccessToken $exception) {
     $accessToken = $tracker->getAccessToken(true); // If the access token is invalid, refresh it.
     $shipment = $tacker->track('CNAQV100168101);
     //... to do
} catch (TrackException $exception) {
    exit('Track error: ' . $exception->getMessage());
}
```
## License
 
The MIT license. See [MIT](https://opensource.org/licenses/MIT)
