![build status](https://travis-ci.org/asiagohan/MonologStackdriverHandler.svg?branch=master)
[![Coverage Status](https://coveralls.io/repos/github/asiagohan/MonologStackdriverHandler/badge.svg?branch=master)](https://coveralls.io/github/asiagohan/MonologStackdriverHandler?branch=master)
# MonologStackdriverHandler
Monolog Stackdriver Handler is Stackdriver handler for Monolog. It will send Stackdriver a log when an app logs something.  
To use this handler, you should have Google Project Id. For more details, check [here](http://www.stackdriver.com/)

## Installation
You can install the latest version with:
```bash
$ composer require asiagohan/monolog-stackdriver-handler
```

### To use with Laravel versions <= 5.5
edit `bootstrap/app.php` as below:
```php
$app->configureMonologUsing(function ($monolog) {
     $stackdriverHandler = new MonologStackdriverHandler\MonologStackdriverHandler('googleProjectId');
     $monolog->pushHandler($stackdriverHandler);
});
```

If you want to change the name of the log or other options,
```php
$app->configureMonologUsing(function ($monolog) {
    $stackdriverHandler = new MonologStackdriverHandler\MonologStackdriverHandler(
       'googleProjectId',
       'logName',
       [
           'resource' => [
               'labels' => [
                   'foo' => 'bar',
               ],
           ],
       ]
    );
     $monolog->pushHandler($stackdriverHandler);
});
```

### To use with Laravel versions >= 5.6
Add a log channel to the `config/logging.php` as below:
```php
'stackdriver' => [
    'driver' => 'monolog',
    'handler' => MonologStackdriverHandler\MonologStackdriverHandler::class,
    'with' => [
        'googleProjectId' => 'googleProjectId',
        'logName' => 'logName',
        'options' => [
            'resource' => [
               'labels' => [
                   'foo' => 'bar',
               ],
           ]
        ]
    ]
]
```
Then make sure to set your `LOG_CHANNEL` env variable to `stackdriver`
