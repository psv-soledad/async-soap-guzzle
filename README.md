# Asynchronous SOAP client

[![Scrutinizer Code Quality](https://scrutinizer-ci.com/g/meng-tian/async-soap-guzzle/badges/quality-score.png?b=master)](https://scrutinizer-ci.com/g/meng-tian/async-soap-guzzle/?branch=master)
An asynchronous SOAP client build on top of Guzzle. The `SoapClient` implements [meng-tian/php-async-soap](https://github.com/meng-tian/php-async-soap)

## Requirement
PHP 5.5 --enablelibxml --enable-soap

## Install
```
composer install meng-tian/async-soap-guzzle
```

## Usage
```php
use GuzzleHttp\Client;
use Meng\AsyncSoap\Guzzle\Factory;
use Meng\Soap\HttpBinding\RequestBuilder;

$factory = new Factory();
$client = $factory->create(new Client(), new RequestBuilder(), 'http://www.webservicex.net/Statistics.asmx?WSDL');

// async call
$promise = $client->callAsync('GetStatistics', [['X' => [1,2,3]]]);
$result = $promise->wait();

// sync call
$result = $client->call('GetStatistics', [['X' => [1,2,3]]]);

// magic method
$promise = $client->GetStatistics(['X' => [1,2,3]]);
$result = $promise->wait();
```