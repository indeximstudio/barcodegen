# PicoPrime\BarcodeGenerator

[![Author](https://secure.gravatar.com/avatar/074618e37f640d13d402830f61092d09?d=identicon&s=50)](https://twitter.com/raffw7912)

Barcode Generator is a simple library that helps you create barcodes images.
It's designed for Laravel 5 and it can create PNG images or DATA-URL strings.

# Installation

Through Composer, obviously:

```
composer require picoprime/barcodegen:@dev
```

or you can edit composer.json file and add `"picoprime/barcodegen": "@dev"` to your "require" section.

# Integrations

Successfully tested in Laravel 5. Steps to make it work:

* edit "require" section in composer.json as described above
* edit config/app.php file and add `PicoPrime\BarcodeGen\BarcodeGenServiceProvider::class,` to providers
* create controller or add new methods to existing controllers (example is in "docs" folder).
You have to use `PicoPrime\BarcodeGen\BarcodeGenerator` in your controllers. It can be injected as well.
Before you call `generate()` method you have to pass variables to `init()` like so:

```
$this->barcode
    ->init($text, $size, $orientation, $codeType)
    ->generate()
```

or

```
$this->barcode
    ->generate($text, $size, $orientation, $codeType)
```

where:

* "text" is the text that you want to transform into barcode,
* "size" is barcode's height in pixels. If you need to change width in the frontend, then CSS is the best for it!
* "orientation" does what it says - changes barcode's orientation. Available: horizontal and vertical,
* "codeType" is the type of code that you want to generate. Available: code128, code128a, code39, code25, codabar.

You can also pass these parameters as assoc or numeric array, like so:

```
$this->barcode
    ->generate(compact('text', 'size', 'orientation', 'codeType'))
```

or

```
$this->barcode
    ->generate(['textToTransform', 50, 'horizontal', 'code128'])
```

Last step to generate image is to send whatever has been generated above to `->response('png')` or `->encode('data-url')`.
Response will create Laravel's response and will display an image, whilst "encode" will create a string.

Please take a look at example controller in `docs` folder.


### Routes

You can create routes as you like. Two examples that we usually use:

```
Route::get('barcode/img/{text}/{size?}/{codeType?}/{orientation?}', 'BarcodeController@barcodeAsPng');
Route::get('barcode/url/{text}/{size?}/{codeType?}/{orientation?}', 'BarcodeController@barcodeAsDataUrl');
```


### Frontend use

Finally to use it in frontend, just use your route in `img` "src" attribute:

```
<img src="/barcode/img/someText" alt="barcode">
```

This example should generate horizontal, 50px, code128 barcode for "someText".


## Issues

We are still in development, so be aware of little bugs that may slip through our fingers.
If you discover any issues, please email raff@picoprime.com instead of using the issue tracker.


# Enjoy

Oh and if you've come down this far, you might as well follow me on [twitter](http://twitter.com/raffw7912)
or check out our company's [website](https://picoprime.com).
