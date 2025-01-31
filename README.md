# Cookies popup 
> Laravel package

This package provides a popup layer to manage cookies consent

[![Latest Version on Packagist](https://img.shields.io/packagist/v/itemvirtual/cookies-popup.svg?style=flat-square)](https://packagist.org/packages/itemvirtual/cookies-popup)
[![Total Downloads](https://img.shields.io/packagist/dt/itemvirtual/cookies-popup.svg?style=flat-square)](https://packagist.org/packages/itemvirtual/cookies-popup)


## Installation

You can install the package via composer:

```bash
composer require itemvirtual/cookies-popup
```

Publish config file (with --force option to update)
```bash
php artisan vendor:publish --provider="Itemvirtual\CookiesPopup\CookiesPopupServiceProvider" --tag=config
```

You need to add package cookies to the `EncryptCookies` except array
```php
# file app/Http/Middleware/EncryptCookies.php
protected $except = [
    'analytical_cookies',
    'advertising_cookies',
    'recaptcha_cookies',
    'preferences_cookies',
];
```

### Generate translations

There is a command to create the required translations in `labels` section
```bash
php artisan cookies-popup:generate-labels
```

If you prefer to create the translations in a file, these are the necessary indexes
```bash
cookies-popup-title
cookies-popup-text
cookies-popup-configure
cookies-popup-accept
accept-required-cookies-label
accept-required-cookies-info
accept-preferences-cookies-label
accept-preferences-cookies-info
accept-analytical-cookies-label
accept-analytical-cookies-info
accept-advertising-cookies-label
accept-advertising-cookies-info
accept-recaptcha-cookies-label
accept-recaptcha-cookies-info
cookies-popup-close
```

## Usage

#### Print popup

To add cookie popup, put this code after footer in your html layout
```
{!! \Itemvirtual\CookiesPopup\CookiesPopup::addCookiesPopup() !!}
```
To add a link to open the cookie popup, use the id `cookies-popup-show` parameter
```html
<a href="#" id="cookies-popup-show">Cookies</a>
```


#### Check if cookies are allowed

To hide or show content related with the cookies consent, use the `allowed` methods
```
@if(\Itemvirtual\CookiesPopup\CookiesPopup::allowedAnalyticalCookies())
@endif
```
```
@if(\Itemvirtual\CookiesPopup\CookiesPopup::allowedAdvertisingCookies())
@endif
```
```
@if(\Itemvirtual\CookiesPopup\CookiesPopup::allowedRecaptchaCookies())
@endif
```
```
@if(\Itemvirtual\CookiesPopup\CookiesPopup::allowedPreferencesCookies())
@endif
```

#### Add Google Analytics scripts

To add the scripts in your layout (`gtag.js` or `analytics.js`), use the method you need ()
```
{!! \Itemvirtual\CookiesPopup\CookiesPopup::getGtagJs() !!}
```
```
{!! \Itemvirtual\CookiesPopup\CookiesPopup::getAnalyticsJs() !!}
```

You need to add an env variable `GA_MEASUREMENT_ID` it can be a comma separated array
```bash
GA_MEASUREMENT_ID="UA-XXXXX-Y"
GA_MEASUREMENT_ID="UA-XXXXX-Y, AW-XXXXXXX"
```

The `analytics.js` script can be normal or `async` script [more info](https://developers.google.com/analytics/devguides/collection/analyticsjs#alternative_async_tag)  

[analytics.js](https://developers.google.com/analytics/devguides/collection/analyticsjs)  
[Universal Analytics (gtag.js)](https://developers.google.com/analytics/devguides/collection/gtagjs)


### Styling

To styling your pop-up window, you have two options.  
The `custom_styles` or `custom_classes` config parameters.  

With `custom_styles` you can change some CSS styles. If you need a deeper design change,
use `custom_classes`, which will concatenate your class to the generic one

### Changelog

Please see [CHANGELOG](CHANGELOG.md) for more information what has changed recently.

## Contributing

Please see [CONTRIBUTING](CONTRIBUTING.md) for details.

## Credits

-   [Sergio](https://github.com/sergio-item)
-   [Itemvirtual](https://github.com/itemvirtual)
-   [All Contributors](../../contributors)

## License

The MIT License (MIT). Please see [License File](LICENSE.md) for more information.
