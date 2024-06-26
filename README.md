[![MIT license](http://img.shields.io/badge/license-MIT-brightgreen.svg)](http://opensource.org/licenses/MIT)
[![Maintenance level: Love](https://img.shields.io/badge/maintenance-%E2%99%A1%E2%99%A1%E2%99%A1-ff69b4.svg)](https://www.flownative.com/en/products/open-source.html)

# Harbor OpenAPI client

This package provides a client for [Harbor](https://goharbor.io/). It was 
auto-generated with [Jane](https://github.com/janephp/janephp) based on the 
Harbor API v2. 

## Feature coverage

This library only provides subset of the resources provided by the Harbor 
API. The included API paths are defined in `.jane-openapi`. If further 
resources are needed, you can adjust the configuration as needed and rebuild 
the client library.

## Rebuilding the client library

Jane provides commands for generating the client code. Switch to this 
package's directory and install Composer dependencies. You can then run a 
command for generating the code: 

```bash
composer update
bin/jane-openapi-generate
```

## Usage

The client is instantiated using the `create()` factory method. The 
following example shows how to create a project, authenticating with 
username and password of a Harbor robot user: 

```php
use Http\Client\Common\Plugin\AddHostPlugin;
use Http\Client\Common\Plugin\AddPathPlugin;
use Http\Client\Common\Plugin\AuthenticationPlugin;
use Http\Message\Authentication\BasicAuth;
use Flownative\Harbor\Api\Model\ProjectReq;

…

$client = \Flownative\Harbor\Api\Client::create(
    null,
    [
        new AddHostPlugin(
            $endpointUri
        ),
        new AddPathPlugin(
            $endpointUri
        ),
        new AuthenticationPlugin(
            new BasicAuth(
                $username,
                $password,
            )
        )
    ]
);

$projectRequest = new ProjectReq();
$projectRequest
    ->setProjectName((string)$projectName)
    ->setPublic(false);

$client->createProject($projectRequest);
```
