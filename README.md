Extract text from a pdf
-----

This package provides a class to extract text from a pdf.

**This is a fork of [Spatie/pdftotext](https://github.com/spatie/pdf-to-text/)**

````php
<?php

use Bakame\Pdftotext\TextExtractor;

$extractor = new TextExtractor('/path/to/pdftotext');
$text = $extractor->toString('/path/to/file.pdf');
````

## Requirements

You need **PHP >= 7.2+** but the latest stable version of PHP is recommended.

Behind the scenes this package leverages [pdftotext](https://en.wikipedia.org/wiki/Pdftotext). You can verify if the binary installed on your system by issueing this command:

```bash
which pdftotext
```

If it is installed it will return the path to the binary.

To install the binary you can use this command on Ubuntu or Debian:

```bash
apt-get install poppler-utils
```

If you're on RedHat or CentOS use this:

```bash
yum install poppler-utils
```

## Installation

You can install the package via composer:

```bash
composer require bakame/pdf-text-extractor
```

## Usage

Extracting text from a pdf is easy, just need to specify:
 
- the path to the `pdftotext` binary.
- the path to the pdf file to extract.

```php
<?php

use Bakame\Pdftotext\TextExtractor;

$text = (new TextExtractor('/path/to/pdftotext'))
    ->toString('/path/to/file.pdf')
;
```

Sometimes you may want to use [pdftotext options](https://linux.die.net/man/1/pdftotext). 
You can add them as options to the `toString` method calls like shown below:

```php
<?php

use Bakame\Pdftotext\TextExtractor;
$text = (new TextExtractor('/path/to/pdftotext'))
    ->toString('table.pdf', ['layout', 'r 96'])
;
```

If you need to add defaults options, you can use the `setDefaultOptions` method to add basic options on each extraction call, or use
the class constructor :
 
 ```php
<?php

use Bakame\Pdftotext\TextExtractor;
$text = (new TextExtractor('/path/to/pdftotext', ['layout', 'r 96']))
    ->toString('table.pdf', ['f 1'])
;
// will return the same data as

$extractor = new TextExtractor('/path/to/pdftotext');
$extractor->setDefaultOptions(['layout', 'r 96']);
$text = $extractor->toString('table.pdf', ['f 1']);
 ```

You can even directly save your text extraction to a file using the `toFile` method. This 
method takes the same arguments as the `toString` method but insert a destination file as its
second argument.

 ```php
<?php

use Bakame\Pdftotext\TextExtractor;

$bytes = (new TextExtractor('/path/to/pdftotext', ['layout', 'r 96']))
    ->toFile('table.pdf', 'table.txt', ['f 1'])
;
 ```
The returned `$bytes` is the number of bytes written to the file.

### Advanced usage

You can set a timeout if you are dealing with larges PDF files using the `setTimeout` method. By default, the timeout is set to 60 seconds.

 ```php
<?php

use Bakame\Pdftotext\TextExtractor;

$extractor = new TextExtractor('/path/to/pdftotext', ['layout', 'r 96']);
$extractor->setTimeout(120); //the extraction will timeout after 2 minutes.
$bytes = $extractor->toFile('table.pdf', 'table.txt', ['f 1']);
 ```

Testing
-------

The package has:

- a coding style compliance test suite using [PHP CS Fixer](http://cs.sensiolabs.org/).
- a code analysis compliance test suite using [PHPStan](https://github.com/phpstan/phpstan).
- a [PHPUnit](https://phpunit.de) test suite

To run the tests, run the following command from the project folder.

``` bash
$ composer test
```

Contributing
-------

Contributions are welcome and will be fully credited. Please see [CONTRIBUTING](.github/CONTRIBUTING.md) and [CONDUCT](CONDUCT.md) for details.

Security
-------

If you discover any security related issues, please email nyamsprod@gmail.com instead of using the issue tracker.

Changelog
-------

Please see [CHANGELOG](CHANGELOG.md) for more information on what has changed recently.

Credits
-------

- [Ignace Nyamagana Butera](https://github.com/nyamsprod)
- [Freek Van der Herten](https://github.com/freekmurze)
- [All Contributors](../../contributors)