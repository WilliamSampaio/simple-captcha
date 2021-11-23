# simple-captcha
Simple class that implement a CAPTCHA for your PHP App.

![GitHub](https://img.shields.io/github/license/WilliamSampaio/simple-captcha)
![GitHub release (latest SemVer)](https://img.shields.io/github/v/release/WilliamSampaio/simple-captcha?logo=github)

## Installation

Use the package manager [composer](https://getcomposer.org/) to install.

```bash
composer require williamsampaio/simple-captcha
```

## Documentation

#### 1. Create new Captcha

```php
 $captcha = new SimpleCaptcha();
```
If no parameters are passed the captcha code will be automatically generated with a length of 5 numeric characters.

But it is possible to pass two parameters. The first is a string with the captcha code (maximum length of 16 characters), the second is a boolean to generate random colors if true.

```php
 $captcha = new SimpleCaptcha("H@ck3R'D_C0@r1", true);
```

#### 2. Get the captcha code

```php
 $captcha->getKey();
```

#### 3. Get the captcha image

```php
<img src="<?php echo $captcha->getImg() ?>" />
```

## Example

A simple usage example.

```php
<?php

require __DIR__ . '/../vendor/autoload.php';

use WilliamSampaio\SimpleCaptcha\SimpleCaptcha;

session_start();

$captcha = new SimpleCaptcha();

if(isset($_POST['captcha'])){

    if($_POST['captcha'] == $_SESSION['captcha']->getKey()){
        echo "<h1 style='color:green;'>Captcha valid! (".$_POST['captcha'] ."=". $_SESSION['captcha']->getKey().")</h1>";
    }else{
        echo "<h1 style='color:red;'>Captcha invalid! (".$_POST['captcha'] ."=". $_SESSION['captcha']->getKey().")</h1>";
    }

}

$_SESSION['captcha'] = $captcha;

?>

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <form method="post">
        <img src="<?= $captcha->getImg() ?>"/>
        <br>
        <input type="text" name="captcha" id="captcha">
        <hr>
        <input type="submit" value="Check">
    </form>
</body>
</html>

```
