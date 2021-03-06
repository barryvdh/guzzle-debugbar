# [Guzzle](http://docs.guzzlephp.org/en/latest/) subscriber to log to [debugbar](https://github.com/maximebf/php-debugbar)'s timeline

Guzzle Subscriber for logging to debugbar's timeline and logs.

![Debugbar timeline](https://www.dropbox.com/s/cabwqycckbu681b/debugbar-timeline.png?dl=1 "Debugbar timeline")
![Debugbar logs](https://www.dropbox.com/s/7rez2q1mbrl76yq/debugbar-logs.png?dl=1 "Debugbar logs")

## Usage

Just four lines of code are needed to log your requests to debugbar's timeline.

```php
$debugBar = new StandardDebugBar();

// Get data collectors.
$timeline = $debugBar->getCollector('time');
$exceptions = $debugBar->getCollector('exceptions');

// Create the subscriber.
$subscriber = new GuzzleHttp\Subscriber\Log\DebugbarSubscriber($timeline, $exceptions);

// Attach it to the Guzzle client's event emitter.
$client = new GuzzleHttp\Client;
$client->getEmitter()->attach($subscriber);
```

Now `$client` is ready to make requests.

Every request is now logged to the timeline, and thrown exceptions are logged to the 'Messages' tab.

### Recommended: use Guzzle's LogSubscriber

```php
$debugBar = new StandardDebugBar();

// PSR-3 logger:
$logger = $debugBar->getCollector('messages');

// Create a new LogSubscriber.
$subscriber = new GuzzleHttp\Subscriber\Log\LogSubscriber($logger);

// Attach it to the Guzzle client's event emitter.
$client = new GuzzleHttp\Client;
$client->getEmitter()->attach($subscriber);
```

## Support

### Laravel 4+

First make sure you have my friend Barry's [laravel-debugbar](https://github.com/barryvdh/laravel-debugbar) configured.
Then include the `GuzzleHttp\Subscriber\Log\Support\Laravel\ServiceProvider` from this package to the app's `providers`
array.

## Contributing

Please be nice in issues/pull request, and stick to PSR-2. Everything will be just fine.
Run tests with `composer test`.

## License

[MIT](license)
