## Chick Mate

ChickMate is a PHP package that detects the gender of a person based on first name. 
It uses the data file from the project 'gender.c' by Jörg Michael (original [link][https://autohotkey.com/board/topic/20260-gender-verification-by-forename-cmd-line-tool-db/]).

### Installation

Install it with Composer

```bash
composer require tuqqu/chickmate
```

### Usage

Its usage is simple, for any given name it will give you one of the following genders (strings): 
`male`, `mostly_male`, `unisex`, `mostly_female`, `female`. 
For an unknown name it will return `null`.
All the gender values are available as constants of the `ChickMate\Gender` class for the convenience. 

```php
<?php 

$genderDetector = new ChickMate\GenderDetector();

print $genderDetector->detect('Thomas');
// male
```

I18N is fully supported

```php
<?php

print $genderDetector->detect('Želmíra');
// female

print $genderDetector->detect('Geirþrúður');
// female
```

You may specify a country or region.

```php
<?php

print $genderDetector->detect('Robin');
// mostly_male

print $genderDetector->detect('Robin', ChickMate\Country::USA);
// mostly_female

print $genderDetector->detect('Robin', ChickMate\Country::FRANCE);
// male

print $genderDetector->detect('Robin', ChickMate\Country::IRELAND);
// unisex
```

All the countries are available as constants of the `ChickMate\Country` class. 
For more details see [country list][/doc/country_list.md].

You may want to override the unknown name value. 
If it is the case, you need to set a new value with `setUnknownGender(string $unknown)` method.

```php
<?php

$genderDetector = new ChickMate\GenderDetector();

print $genderDetector->detect('Doe');
// (null)

$genderDetector->setUnknownGender(ChickMate\Gender::UNISEX);

print $genderDetector->detect('Doe');
// unisex
```

If you happen to have an alternative data file, you might pass it to the `GenderDetector` constructor's first argument. 
Additionally you may add new dictionary files with `addDictionaryFile(string $path)` method. 

```php
<?php

$genderDetector = new ChickMate\GenderDetector('custom_file_path/dict.txt');
$genderDetector->addDictionaryFile('custom_file_path/another_dict.txt');
```

Each file will be parsed only once, so you need not worry about instantiating many `GenderDetector`'s.

### Licenses

The `ChickMate` is licensed under the GNU General Public License v3.0.

The data file `data/nam_dict.txt` is licensed under the GNU Free Documentation License.