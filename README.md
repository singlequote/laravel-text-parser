# Easy text parser

[![Latest Version on Packagist](https://img.shields.io/packagist/v/Quotecnl/parser.svg?style=flat-square)](https://packagist.org/packages/Quotecnl/Parser)
[![Total Downloads](https://img.shields.io/packagist/dt/Quotecnl/parser.svg?style=flat-square)](https://packagist.org/packages/Quotecnl/Parser)


A package to replace words in a text with values from a array. Also supports aliases and excluded properties.

## Installation

You can install the package via composer:

```bash
composer require Quotecnl/Parser
```

## Basic Usage

``` php
Parser::text('Hello [who]')->values(['who' => 'world'])->parse(); // Hello world

Parser::text('Hello {who}')->values(['who' => 'world'])->tags(['{', '}'])->parse(); // Hello world

Parser::text('Hello [who]')->values(['who' => 'world'])->exclude(['who'])->parse(); // Hello [who]

Parser::text('Hello [what]')->values(['who' => 'world'])->aliases(['what' => 'who'])->parse(); // Hello world
```


### Using arrays as values

```php
$values = [
    'user' => [
        'name' => [
            'first_name' => 'Foo',
            'last_name' => 'Bar'
        ],
        'email' => 'example@example.com'
    ]
];

$input = "[user.name.first_name][user.name.last_name] - [user.email]";

$result = Parser::text($input)->values($values)->parse();
```

will generate `FooBar - example@example.com`


## Available methods

All methods can be chained together like `text()->values()->aliases()` and can be in any order.
But you always have to start with the `text()` function.

### text
This sets the string you want to parse
``` php
    $parser = Parser::text('string')
```

### values
This sets the values to use while parsing. Must be a array
``` php
    $parser->values([]);
```

### tags
Tags are the characters around the keys you want to parse. Default `[` and `]`
``` php
    $parser->tags(['{','}']);
```

### exclude
Sets the keys which are excluded from parsing
``` php
    $parser->exclude(['key', 'key2']);
```

### aliases
Sets the aliases. Aliases can be used to map a value to a different name. 
So for example you can set the aliases to `['name' => 'username']` to map `username` to `name`
``` php
    $parser->exclude(['alias', 'value key']);
```

### parse
Parses the text and returns the parsed string
``` php
    $parser->exclude(['alias', 'value key']);
```

### Testing

``` bash
composer test
```

### Changelog

Please see [CHANGELOG](CHANGELOG.md) for more information what has changed recently.

## Contributing

Please see [CONTRIBUTING](CONTRIBUTING.md) for details.

### Security

If you discover any security related issues, please email info@Quotecnl.nl instead of using the issue tracker.


## Credits

- [Quotec](https://github.com/quotecnl)
- [All Contributors](../../contributors)


## License

The MIT License (MIT). Please see [License File](LICENSE.md) for more information.
