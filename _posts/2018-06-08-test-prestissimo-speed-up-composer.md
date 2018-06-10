---
layout: post
title: Test prestissimo speed up composer
date: 2018-06-08 10:13 +0000
---

# Without prestissimo
## Run docker env
```
docker run -it --rm dockercraft/composer

```


## In docker env
```
# date && composer create-project laravel/laravel laravel1 && date
```

```
Fri Jun  8 00:10:53 UTC 2018
Installing laravel/laravel (v5.6.21)
  - Installing laravel/laravel (v5.6.21): Downloading (100%)
Created project in laravel1
> @php -r "file_exists('.env') || copy('.env.example', '.env');"
Loading composer repositories with package information
Updating dependencies (including require-dev)
Package operations: 70 installs, 0 updates, 0 removals
  - Installing vlucas/phpdotenv (v2.4.0): Downloading (100%)
  - Installing symfony/css-selector (v4.1.0): Downloading (100%)
  - Installing tijsverkoyen/css-to-inline-styles (2.2.1): Downloading (100%)
  - Installing symfony/polyfill-php72 (v1.8.0): Downloading (100%)
  - Installing symfony/polyfill-mbstring (v1.8.0): Downloading (100%)
  - Installing symfony/var-dumper (v4.1.0): Downloading (100%)
  - Installing symfony/routing (v4.1.0): Downloading (100%)
  - Installing symfony/process (v4.1.0): Downloading (100%)
  - Installing symfony/polyfill-ctype (v1.8.0): Downloading (100%)
  - Installing symfony/http-foundation (v4.1.0): Downloading (100%)
  - Installing symfony/event-dispatcher (v4.1.0): Downloading (100%)
  - Installing psr/log (1.0.2): Downloading (100%)
  - Installing symfony/debug (v4.1.0): Downloading (100%)
  - Installing symfony/http-kernel (v4.1.0): Downloading (100%)
  - Installing paragonie/random_compat (v2.0.14): Downloading (100%)
  - Installing symfony/finder (v4.1.0): Downloading (100%)
  - Installing symfony/console (v4.1.0): Downloading (100%)
  - Installing doctrine/lexer (v1.0.1): Downloading (100%)
  - Installing egulias/email-validator (2.1.4): Downloading (100%)
  - Installing swiftmailer/swiftmailer (v6.0.2): Downloading (100%)
  - Installing ramsey/uuid (3.7.3): Downloading (100%)
  - Installing psr/simple-cache (1.0.1): Downloading (100%)
  - Installing psr/container (1.0.0): Downloading (100%)
  - Installing symfony/translation (v4.1.0): Downloading (100%)
  - Installing nesbot/carbon (1.25.0): Downloading (100%)
  - Installing monolog/monolog (1.23.0): Downloading (100%)
  - Installing league/flysystem (1.0.45): Downloading (100%)
  - Installing erusev/parsedown (1.7.1): Downloading (100%)
  - Installing dragonmantank/cron-expression (v2.2.0): Downloading (100%)
  - Installing doctrine/inflector (v1.3.0): Downloading (100%)
  - Installing laravel/framework (v5.6.24): Downloading (100%)
  - Installing fideloper/proxy (4.0.0): Downloading (100%)
  - Installing nikic/php-parser (v4.0.2): Downloading (100%)
  - Installing jakub-onderka/php-console-color (0.1): Downloading (100%)
  - Installing jakub-onderka/php-console-highlighter (v0.3.2): Downloading (100%)
  - Installing dnoegel/php-xdg-base-dir (0.1): Downloading (100%)
  - Installing psy/psysh (v0.9.5): Downloading (100%)
  - Installing laravel/tinker (v1.0.7): Downloading (100%)
  - Installing fzaninotto/faker (v1.7.1): Downloading (100%)
  - Installing hamcrest/hamcrest-php (v2.0.0): Downloading (100%)
  - Installing mockery/mockery (1.1.0): Downloading (100%)
  - Installing filp/whoops (2.2.0): Downloading (100%)
  - Installing nunomaduro/collision (v2.0.2): Downloading (100%)
  - Installing sebastian/version (2.0.1): Downloading (100%)
  - Installing sebastian/resource-operations (1.0.0): Downloading (100%)
  - Installing sebastian/object-reflector (1.1.1): Downloading (100%)
  - Installing sebastian/recursion-context (3.0.0): Downloading (100%)
  - Installing sebastian/object-enumerator (3.0.3): Downloading (100%)
  - Installing sebastian/global-state (2.0.0): Downloading (100%)
  - Installing sebastian/exporter (3.1.0): Downloading (100%)
  - Installing sebastian/environment (3.1.0): Downloading (100%)
  - Installing sebastian/diff (3.0.0): Downloading (100%)
  - Installing sebastian/comparator (3.0.0): Downloading (100%)
  - Installing phpunit/php-timer (2.0.0): Downloading (100%)
  - Installing phpunit/php-text-template (1.2.1): Downloading (100%)
  - Installing phpunit/php-file-iterator (2.0.0): Downloading (100%)
  - Installing theseer/tokenizer (1.1.0): Downloading (100%)
  - Installing sebastian/code-unit-reverse-lookup (1.0.1): Downloading (100%)
  - Installing phpunit/php-token-stream (3.0.0): Downloading (100%)
  - Installing phpunit/php-code-coverage (6.0.7): Downloading (100%)
  - Installing doctrine/instantiator (1.1.0): Downloading (100%)
  - Installing webmozart/assert (1.3.0): Downloading (100%)
  - Installing phpdocumentor/reflection-common (1.0.1): Downloading (100%)
  - Installing phpdocumentor/type-resolver (0.4.0): Downloading (100%)
  - Installing phpdocumentor/reflection-docblock (4.3.0): Downloading (100%)
  - Installing phpspec/prophecy (1.7.6): Downloading (100%)
  - Installing phar-io/version (1.0.1): Downloading (100%)
  - Installing phar-io/manifest (1.0.1): Downloading (100%)
  - Installing myclabs/deep-copy (1.8.0): Downloading (100%)
  - Installing phpunit/phpunit (7.2.4): Downloading (100%)
symfony/var-dumper suggests installing ext-intl (To show region name in time zone dump)
symfony/routing suggests installing doctrine/annotations (For using the annotation loader)
symfony/routing suggests installing symfony/config (For using the all-in-one router or any loader)
symfony/routing suggests installing symfony/dependency-injection (For loading routes from a service)
symfony/routing suggests installing symfony/expression-language (For using expression matching)
symfony/routing suggests installing symfony/yaml (For using the YAML loader)
symfony/event-dispatcher suggests installing symfony/dependency-injection ()
symfony/http-kernel suggests installing symfony/browser-kit ()
symfony/http-kernel suggests installing symfony/config ()
symfony/http-kernel suggests installing symfony/dependency-injection ()
paragonie/random_compat suggests installing ext-libsodium (Provides a modern crypto API that can be used to generate random bytes.)
symfony/console suggests installing symfony/lock ()
egulias/email-validator suggests installing ext-intl (PHP Internationalization Libraries are required to use the SpoofChecking validation)
ramsey/uuid suggests installing ircmaxell/random-lib (Provides RandomLib for use with the RandomLibAdapter)
ramsey/uuid suggests installing ext-libsodium (Provides the PECL libsodium extension for use with the SodiumRandomGenerator)
ramsey/uuid suggests installing ext-uuid (Provides the PECL UUID extension for use with the PeclUuidTimeGenerator and PeclUuidRandomGenerator)
ramsey/uuid suggests installing moontoast/math (Provides support for converting UUID to 128-bit integer (in string form).)
ramsey/uuid suggests installing ramsey/uuid-doctrine (Allows the use of Ramsey\Uuid\Uuid as Doctrine field type.)
ramsey/uuid suggests installing ramsey/uuid-console (A console application for generating UUIDs with ramsey/uuid)
symfony/translation suggests installing symfony/config ()
symfony/translation suggests installing symfony/yaml ()
monolog/monolog suggests installing aws/aws-sdk-php (Allow sending log messages to AWS services like DynamoDB)
monolog/monolog suggests installing doctrine/couchdb (Allow sending log messages to a CouchDB server)
monolog/monolog suggests installing ext-amqp (Allow sending log messages to an AMQP server (1.0+ required))
monolog/monolog suggests installing ext-mongo (Allow sending log messages to a MongoDB server)
monolog/monolog suggests installing graylog2/gelf-php (Allow sending log messages to a GrayLog2 server)
monolog/monolog suggests installing mongodb/mongodb (Allow sending log messages to a MongoDB server via PHP Driver)
monolog/monolog suggests installing php-amqplib/php-amqplib (Allow sending log messages to an AMQP server using php-amqplib)
monolog/monolog suggests installing php-console/php-console (Allow sending log messages to Google Chrome)
monolog/monolog suggests installing rollbar/rollbar (Allow sending log messages to Rollbar)
monolog/monolog suggests installing ruflin/elastica (Allow sending log messages to an Elastic Search server)
monolog/monolog suggests installing sentry/sentry (Allow sending log messages to a Sentry server)
league/flysystem suggests installing ext-ftp (Allows you to use FTP server storage)
league/flysystem suggests installing league/flysystem-aws-s3-v2 (Allows you to use S3 storage with AWS SDK v2)
league/flysystem suggests installing league/flysystem-aws-s3-v3 (Allows you to use S3 storage with AWS SDK v3)
league/flysystem suggests installing league/flysystem-azure (Allows you to use Windows Azure Blob storage)
league/flysystem suggests installing league/flysystem-cached-adapter (Flysystem adapter decorator for metadata caching)
league/flysystem suggests installing league/flysystem-eventable-filesystem (Allows you to use EventableFilesystem)
league/flysystem suggests installing league/flysystem-rackspace (Allows you to use Rackspace Cloud Files)
league/flysystem suggests installing league/flysystem-sftp (Allows you to use SFTP server storage via phpseclib)
league/flysystem suggests installing league/flysystem-webdav (Allows you to use WebDAV storage)
league/flysystem suggests installing league/flysystem-ziparchive (Allows you to use ZipArchive adapter)
league/flysystem suggests installing spatie/flysystem-dropbox (Allows you to use Dropbox storage)
league/flysystem suggests installing srmklive/flysystem-dropbox-v2 (Allows you to use Dropbox storage for PHP 5 applications)
laravel/framework suggests installing aws/aws-sdk-php (Required to use the SQS queue driver and SES mail driver (~3.0).)
laravel/framework suggests installing doctrine/dbal (Required to rename columns and drop SQLite columns (~2.6).)
laravel/framework suggests installing ext-pcntl (Required to use all features of the queue worker.)
laravel/framework suggests installing ext-posix (Required to use all features of the queue worker.)
laravel/framework suggests installing guzzlehttp/guzzle (Required to use the Mailgun and Mandrill mail drivers and the ping methods on schedules (~6.0).)
laravel/framework suggests installing league/flysystem-aws-s3-v3 (Required to use the Flysystem S3 driver (~1.0).)
laravel/framework suggests installing league/flysystem-cached-adapter (Required to use the Flysystem cache (~1.0).)
laravel/framework suggests installing league/flysystem-rackspace (Required to use the Flysystem Rackspace driver (~1.0).)
laravel/framework suggests installing league/flysystem-sftp (Required to use the Flysystem SFTP driver (~1.0).)
laravel/framework suggests installing nexmo/client (Required to use the Nexmo transport (~1.0).)
laravel/framework suggests installing pda/pheanstalk (Required to use the beanstalk queue driver (~3.0).)
laravel/framework suggests installing predis/predis (Required to use the redis cache and queue drivers (~1.0).)
laravel/framework suggests installing pusher/pusher-php-server (Required to use the Pusher broadcast driver (~3.0).)
laravel/framework suggests installing symfony/dom-crawler (Required to use most of the crawler integration testing tools (~4.0).)
laravel/framework suggests installing symfony/psr-http-message-bridge (Required to psr7 bridging features (~1.0).)
psy/psysh suggests installing ext-pcntl (Enabling the PCNTL extension makes PsySH a lot happier :))
psy/psysh suggests installing ext-posix (If you have PCNTL, you'll want the POSIX extension as well.)
psy/psysh suggests installing ext-pdo-sqlite (The doc command requires SQLite to work.)
psy/psysh suggests installing hoa/console (A pure PHP readline implementation. You'll want this if your PHP install doesn't already support readline or libedit.)
filp/whoops suggests installing whoops/soap (Formats errors as SOAP responses)
sebastian/global-state suggests installing ext-uopz (*)
phpunit/php-code-coverage suggests installing ext-xdebug (^2.6.0)
phpunit/phpunit suggests installing phpunit/php-invoker (^2.0)
phpunit/phpunit suggests installing ext-soap (*)
phpunit/phpunit suggests installing ext-xdebug (*)
Writing lock file
Generating optimized autoload files
> Illuminate\Foundation\ComposerScripts::postAutoloadDump
> @php artisan package:discover
Discovered Package: fideloper/proxy
Discovered Package: laravel/tinker
Discovered Package: nunomaduro/collision
Package manifest generated successfully.
> @php artisan key:generate
Application key [base64:dXlhlvlSfHVdF9dlCUTfEJpWxYrqKJHKjv8McPyS0Pc=] set successfully.
Fri Jun  8 00:18:41 UTC 2018
```


from `Fri Jun  8 00:10:53 UTC 2018` to `Fri Jun  8 00:18:41 UTC 2018`



# With prestissimo

```
composer global require hirak/prestissimo
date && composer create-project laravel/laravel laravel1 && date
```


```
Fri Jun  8 00:30:02 UTC 2018
    1/1:  http://packagist.org/p/provider-latest$608b74a9d05b383f3b34e67a88df34c31cd9470c1db7363b06fef65fc41446b5.json
    Finished: success: 1, skipped: 0, failure: 0, total: 1
Installing laravel/laravel (v5.6.21)
  - Installing laravel/laravel (v5.6.21): Downloading (100%)
Created project in laravel1
> @php -r "file_exists('.env') || copy('.env.example', '.env');"
Loading composer repositories with package information
Updating dependencies (including require-dev)
    1/70: https://codeload.github.com/webmozart/assert/legacy.zip/0df1908962e7a3071564e857d86874dad1ef204a
    2/70: https://codeload.github.com/phpDocumentor/ReflectionCommon/legacy.zip/21bdeb5f65d7ebf9f43b1b25d404f87deab5bfb6
    3/70: https://codeload.github.com/doctrine/instantiator/legacy.zip/185b8868aa9bf7159f5f953ed5afb2d7fcdc3bda
    4/70: https://codeload.github.com/phpDocumentor/TypeResolver/legacy.zip/9c977708995954784726e25d0cd1dddf4e65b0f7
    5/70: https://codeload.github.com/phar-io/version/legacy.zip/a70c0ced4be299a63d32fa96d9281d03e94041df
    6/70: https://codeload.github.com/sebastianbergmann/code-unit-reverse-lookup/legacy.zip/4419fcdb5eabb9caa61a27c7a1db532a6b55dd18
    7/70: https://codeload.github.com/myclabs/DeepCopy/legacy.zip/478465659fd987669df0bd8a9bf22a8710e5f1b6
    8/70: https://codeload.github.com/theseer/tokenizer/legacy.zip/cb2f008f3f05af2893a87208fe6a6c4985483f8b
    9/70: https://codeload.github.com/phar-io/manifest/legacy.zip/2df402786ab5368a0169091f61a7c1e0eb6852d0
    10/70:  https://codeload.github.com/phpDocumentor/ReflectionDocBlock/legacy.zip/94fd0001232e47129dd3504189fa1c7225010d08
    11/70:  https://codeload.github.com/sebastianbergmann/php-token-stream/legacy.zip/21ad88bbba7c3d93530d93994e0a33cd45f02ace
    12/70:  https://codeload.github.com/sebastianbergmann/php-file-iterator/legacy.zip/e20525b0c2945c7c317fff95660698cb3d2a53bc
    13/70:  https://codeload.github.com/sebastianbergmann/php-text-template/legacy.zip/31f8b717e51d9a2afca6c9f046f5d69fc27c8686
    14/70:  https://codeload.github.com/phpspec/prophecy/legacy.zip/33a7e3c4fda54e912ff6338c48823bd5c0f0b712
    15/70:  https://codeload.github.com/sebastianbergmann/php-timer/legacy.zip/8b8454ea6958c3dee38453d3bd571e023108c91f
    16/70:  https://codeload.github.com/sebastianbergmann/environment/legacy.zip/cd0871b3975fb7fc44d11314fd1ee20925fce4f5
    17/70:  https://codeload.github.com/sebastianbergmann/exporter/legacy.zip/234199f4528de6d12aaa58b612e98f7d36adb937
    18/70:  https://codeload.github.com/sebastianbergmann/global-state/legacy.zip/e8ba02eed7bbbb9e59e43dedd3dddeff4a56b0c4
    19/70:  https://codeload.github.com/sebastianbergmann/object-enumerator/legacy.zip/7cfd9e65d11ffb5af41198476395774d4c8a84c5
    20/70:  https://codeload.github.com/sebastianbergmann/recursion-context/legacy.zip/5b0cd723502bac3b006cbf3dbf7a1e3fcefe4fa8
    21/70:  https://codeload.github.com/sebastianbergmann/resource-operations/legacy.zip/ce990bb21759f94aeafd30209e8cfcdfa8bc3f52
    22/70:  https://codeload.github.com/sebastianbergmann/object-reflector/legacy.zip/773f97c67f28de00d397be301821b06708fca0be
    23/70:  https://codeload.github.com/sebastianbergmann/version/legacy.zip/99732be0ddb3361e16ad77b68ba41efc8e979019
    24/70:  https://codeload.github.com/nunomaduro/collision/legacy.zip/245958b02c6a9edf24627380f368333ac5413a51
    25/70:  https://codeload.github.com/laravel/tinker/legacy.zip/e3086ee8cb1f54a39ae8dcb72d1c37d10128997d
    26/70:  https://codeload.github.com/filp/whoops/legacy.zip/181c4502d8f34db7aed7bfe88d4f87875b8e947a
    27/70:  https://codeload.github.com/sebastianbergmann/phpunit/legacy.zip/00bc0b93f0ff4f557e9ea766557fde96da9a03dd
    28/70:  https://codeload.github.com/dnoegel/php-xdg-base-dir/legacy.zip/265b8593498b997dc2d31e75b89f053b5cc9621a
    29/70:  https://codeload.github.com/sebastianbergmann/comparator/legacy.zip/ed5fd2281113729f1ebcc64d101ad66028aeb3d5
    30/70:  https://codeload.github.com/JakubOnderka/PHP-Console-Highlighter/legacy.zip/7daa75df45242c8d5b75a22c00a201e7954e4fb5
    31/70:  https://codeload.github.com/hamcrest/hamcrest-php/legacy.zip/776503d3a8e85d4f9a1148614f95b7a608b046ad
    32/70:  https://codeload.github.com/JakubOnderka/PHP-Console-Color/legacy.zip/e0b393dacf7703fc36a4efc3df1435485197e6c1
    33/70:  https://codeload.github.com/mockery/mockery/legacy.zip/99e29d3596b16dabe4982548527d5ddf90232e99
    34/70:  https://codeload.github.com/fideloper/TrustedProxy/legacy.zip/cf8a0ca4b85659b9557e206c90110a6a4dba980a
    35/70:  https://codeload.github.com/dragonmantank/cron-expression/legacy.zip/92a2c3768d50e21a1f26a53cb795ce72806266c5
    36/70:  https://codeload.github.com/doctrine/inflector/legacy.zip/5527a48b7313d15261292c149e55e26eae771b0a
    37/70:  https://codeload.github.com/sebastianbergmann/diff/legacy.zip/e09160918c66281713f1c324c1f4c4c3037ba1e8
    38/70:  https://codeload.github.com/erusev/parsedown/legacy.zip/92e9c27ba0e74b8b028b111d1b6f956a15c01fc1
    39/70:  https://codeload.github.com/thephpleague/flysystem/legacy.zip/a99f94e63b512d75f851b181afcdf0ee9ebef7e6
    40/70:  https://codeload.github.com/php-fig/simple-cache/legacy.zip/408d5eafb83c57f6365a3ca330ff23aa4a5fa39b
    41/70:  https://codeload.github.com/briannesbitt/Carbon/legacy.zip/cbcf13da0b531767e39eb86e9687f5deba9857b4
    42/70:  https://codeload.github.com/php-fig/container/legacy.zip/b7ce3b176482dbbc1245ebf52b181af44c2cf55f
    43/70:  https://codeload.github.com/sebastianbergmann/php-code-coverage/legacy.zip/865662550c384bc1db7e51d29aeda1c2c161d69a
    44/70:  https://codeload.github.com/symfony/translation/legacy.zip/16328f5b217cebc8dd4adfe4aeeaa8c377581f5a
    45/70:  https://codeload.github.com/egulias/EmailValidator/legacy.zip/8790f594151ca6a2010c6218e09d96df67173ad3
    46/70:  https://codeload.github.com/Seldaek/monolog/legacy.zip/fd8c787753b3a2ad11bc60c063cff1358a32a3b4
    47/70:  https://codeload.github.com/doctrine/lexer/legacy.zip/83893c552fd2045dd78aef794c31e694c37c0b8c
    48/70:  https://codeload.github.com/ramsey/uuid/legacy.zip/44abcdad877d9a46685a3a4d221e3b2c4b87cb76
    49/70:  https://codeload.github.com/bobthecow/psysh/legacy.zip/0951e91ac04ca28cf317f3997a0adfc319e80106
    50/70:  https://codeload.github.com/nikic/PHP-Parser/legacy.zip/35b8caf75e791ba1b2d24fec1552168d72692b12
    51/70:  https://codeload.github.com/php-fig/log/legacy.zip/4ebe3a8bf773a19edfe0a84b6585ba3d401b724d
    52/70:  https://codeload.github.com/paragonie/random_compat/legacy.zip/f6ce7dd93628088e1017fb5dd73b0b9fec7df9e5
    53/70:  https://codeload.github.com/symfony/debug/legacy.zip/449f8b00b28ab6e6912c3e6b920406143b27193b
    54/70:  https://codeload.github.com/symfony/event-dispatcher/legacy.zip/2391ed210a239868e7256eb6921b1bd83f3087b5
    55/70:  https://codeload.github.com/symfony/polyfill-ctype/legacy.zip/7cc359f1b7b80fc25ed7796be7d96adc9b354bae
    56/70:  https://codeload.github.com/symfony/process/legacy.zip/73445bd33b0d337c060eef9652b94df72b6b3434
    57/70:  https://codeload.github.com/symfony/polyfill-mbstring/legacy.zip/3296adf6a6454a050679cde90f95350ad604b171
    58/70:  https://codeload.github.com/symfony/finder/legacy.zip/087e2ee0d74464a4c6baac4e90417db7477dc238
    59/70:  https://codeload.github.com/symfony/polyfill-php72/legacy.zip/a4576e282d782ad82397f3e4ec1df8e0f0cafb46
    60/70:  https://codeload.github.com/symfony/var-dumper/legacy.zip/bc88ad53e825ebacc7b190bbd360781fce381c64
    61/70:  https://codeload.github.com/symfony/http-foundation/legacy.zip/a916c88390fb861ee21f12a92b107d51bb68af99
    62/70:  https://codeload.github.com/tijsverkoyen/CssToInlineStyles/legacy.zip/0ed4a2ea4e0902dac0489e6436ebcd5bbcae9757
    63/70:  https://codeload.github.com/vlucas/phpdotenv/legacy.zip/3cc116adbe4b11be5ec557bf1d24dc5e3a21d18c
    64/70:  https://codeload.github.com/symfony/console/legacy.zip/2d5d973bf9933d46802b01010bd25c800c87c242
    65/70:  https://codeload.github.com/symfony/routing/legacy.zip/180b51c66d10f09e562c9ebc395b39aacb2cf8a2
    66/70:  https://codeload.github.com/symfony/css-selector/legacy.zip/03ac71606ecb0b0ce792faa17d74cc32c2949ef4
    67/70:  https://codeload.github.com/symfony/http-kernel/legacy.zip/b5ab9d4cdbfd369083744b6b5dfbf454e31e5f90
    68/70:  https://codeload.github.com/swiftmailer/swiftmailer/legacy.zip/412333372fb6c8ffb65496a2bbd7321af75733fc
    69/70:  https://codeload.github.com/laravel/framework/legacy.zip/56290edeb0d8051826d40b4cbd8ed3c30348b2b5
    70/70:  https://codeload.github.com/fzaninotto/Faker/legacy.zip/d3ed4cc37051c1ca52d22d76b437d14809fc7e0d
    Finished: success: 70, skipped: 0, failure: 0, total: 70
Package operations: 70 installs, 0 updates, 0 removals
  - Installing vlucas/phpdotenv (v2.4.0): Loading from cache
  - Installing symfony/css-selector (v4.1.0): Loading from cache
  - Installing tijsverkoyen/css-to-inline-styles (2.2.1): Loading from cache
  - Installing symfony/polyfill-php72 (v1.8.0): Loading from cache
  - Installing symfony/polyfill-mbstring (v1.8.0): Loading from cache
  - Installing symfony/var-dumper (v4.1.0): Loading from cache
  - Installing symfony/routing (v4.1.0): Loading from cache
  - Installing symfony/process (v4.1.0): Loading from cache
  - Installing symfony/polyfill-ctype (v1.8.0): Loading from cache
  - Installing symfony/http-foundation (v4.1.0): Loading from cache
  - Installing symfony/event-dispatcher (v4.1.0): Loading from cache
  - Installing psr/log (1.0.2): Loading from cache
  - Installing symfony/debug (v4.1.0): Loading from cache
  - Installing symfony/http-kernel (v4.1.0): Loading from cache
  - Installing paragonie/random_compat (v2.0.14): Loading from cache
  - Installing symfony/finder (v4.1.0): Loading from cache
  - Installing symfony/console (v4.1.0): Loading from cache
  - Installing doctrine/lexer (v1.0.1): Loading from cache
  - Installing egulias/email-validator (2.1.4): Loading from cache
  - Installing swiftmailer/swiftmailer (v6.0.2): Loading from cache
  - Installing ramsey/uuid (3.7.3): Loading from cache
  - Installing psr/simple-cache (1.0.1): Loading from cache
  - Installing psr/container (1.0.0): Loading from cache
  - Installing symfony/translation (v4.1.0): Loading from cache
  - Installing nesbot/carbon (1.25.0): Loading from cache
  - Installing monolog/monolog (1.23.0): Loading from cache
  - Installing league/flysystem (1.0.45): Loading from cache
  - Installing erusev/parsedown (1.7.1): Loading from cache
  - Installing dragonmantank/cron-expression (v2.2.0): Loading from cache
  - Installing doctrine/inflector (v1.3.0): Loading from cache
  - Installing laravel/framework (v5.6.24): Loading from cache
  - Installing fideloper/proxy (4.0.0): Loading from cache
  - Installing nikic/php-parser (v4.0.2): Loading from cache
  - Installing jakub-onderka/php-console-color (0.1): Loading from cache
  - Installing jakub-onderka/php-console-highlighter (v0.3.2): Loading from cache
  - Installing dnoegel/php-xdg-base-dir (0.1): Loading from cache
  - Installing psy/psysh (v0.9.5): Loading from cache
  - Installing laravel/tinker (v1.0.7): Loading from cache
  - Installing fzaninotto/faker (v1.7.1): Loading from cache
  - Installing hamcrest/hamcrest-php (v2.0.0): Loading from cache
  - Installing mockery/mockery (1.1.0): Loading from cache
  - Installing filp/whoops (2.2.0): Loading from cache
  - Installing nunomaduro/collision (v2.0.2): Loading from cache
  - Installing sebastian/version (2.0.1): Loading from cache
  - Installing sebastian/resource-operations (1.0.0): Loading from cache
  - Installing sebastian/object-reflector (1.1.1): Loading from cache
  - Installing sebastian/recursion-context (3.0.0): Loading from cache
  - Installing sebastian/object-enumerator (3.0.3): Loading from cache
  - Installing sebastian/global-state (2.0.0): Loading from cache
  - Installing sebastian/exporter (3.1.0): Loading from cache
  - Installing sebastian/environment (3.1.0): Loading from cache
  - Installing sebastian/diff (3.0.0): Loading from cache
  - Installing sebastian/comparator (3.0.0): Loading from cache
  - Installing phpunit/php-timer (2.0.0): Loading from cache
  - Installing phpunit/php-text-template (1.2.1): Loading from cache
  - Installing phpunit/php-file-iterator (2.0.0): Loading from cache
  - Installing theseer/tokenizer (1.1.0): Loading from cache
  - Installing sebastian/code-unit-reverse-lookup (1.0.1): Loading from cache
  - Installing phpunit/php-token-stream (3.0.0): Loading from cache
  - Installing phpunit/php-code-coverage (6.0.7): Loading from cache
  - Installing doctrine/instantiator (1.1.0): Loading from cache
  - Installing webmozart/assert (1.3.0): Loading from cache
  - Installing phpdocumentor/reflection-common (1.0.1): Loading from cache
  - Installing phpdocumentor/type-resolver (0.4.0): Loading from cache
  - Installing phpdocumentor/reflection-docblock (4.3.0): Loading from cache
  - Installing phpspec/prophecy (1.7.6): Loading from cache
  - Installing phar-io/version (1.0.1): Loading from cache
  - Installing phar-io/manifest (1.0.1): Loading from cache
  - Installing myclabs/deep-copy (1.8.0): Loading from cache
  - Installing phpunit/phpunit (7.2.4): Loading from cache
symfony/var-dumper suggests installing ext-intl (To show region name in time zone dump)
symfony/routing suggests installing doctrine/annotations (For using the annotation loader)
symfony/routing suggests installing symfony/config (For using the all-in-one router or any loader)
symfony/routing suggests installing symfony/dependency-injection (For loading routes from a service)
symfony/routing suggests installing symfony/expression-language (For using expression matching)
symfony/routing suggests installing symfony/yaml (For using the YAML loader)
symfony/event-dispatcher suggests installing symfony/dependency-injection ()
symfony/http-kernel suggests installing symfony/browser-kit ()
symfony/http-kernel suggests installing symfony/config ()
symfony/http-kernel suggests installing symfony/dependency-injection ()
paragonie/random_compat suggests installing ext-libsodium (Provides a modern crypto API that can be used to generate random bytes.)
symfony/console suggests installing symfony/lock ()
egulias/email-validator suggests installing ext-intl (PHP Internationalization Libraries are required to use the SpoofChecking validation)
ramsey/uuid suggests installing ircmaxell/random-lib (Provides RandomLib for use with the RandomLibAdapter)
ramsey/uuid suggests installing ext-libsodium (Provides the PECL libsodium extension for use with the SodiumRandomGenerator)
ramsey/uuid suggests installing ext-uuid (Provides the PECL UUID extension for use with the PeclUuidTimeGenerator and PeclUuidRandomGenerator)
ramsey/uuid suggests installing moontoast/math (Provides support for converting UUID to 128-bit integer (in string form).)
ramsey/uuid suggests installing ramsey/uuid-doctrine (Allows the use of Ramsey\Uuid\Uuid as Doctrine field type.)
ramsey/uuid suggests installing ramsey/uuid-console (A console application for generating UUIDs with ramsey/uuid)
symfony/translation suggests installing symfony/config ()
symfony/translation suggests installing symfony/yaml ()
monolog/monolog suggests installing aws/aws-sdk-php (Allow sending log messages to AWS services like DynamoDB)
monolog/monolog suggests installing doctrine/couchdb (Allow sending log messages to a CouchDB server)
monolog/monolog suggests installing ext-amqp (Allow sending log messages to an AMQP server (1.0+ required))
monolog/monolog suggests installing ext-mongo (Allow sending log messages to a MongoDB server)
monolog/monolog suggests installing graylog2/gelf-php (Allow sending log messages to a GrayLog2 server)
monolog/monolog suggests installing mongodb/mongodb (Allow sending log messages to a MongoDB server via PHP Driver)
monolog/monolog suggests installing php-amqplib/php-amqplib (Allow sending log messages to an AMQP server using php-amqplib)
monolog/monolog suggests installing php-console/php-console (Allow sending log messages to Google Chrome)
monolog/monolog suggests installing rollbar/rollbar (Allow sending log messages to Rollbar)
monolog/monolog suggests installing ruflin/elastica (Allow sending log messages to an Elastic Search server)
monolog/monolog suggests installing sentry/sentry (Allow sending log messages to a Sentry server)
league/flysystem suggests installing ext-ftp (Allows you to use FTP server storage)
league/flysystem suggests installing league/flysystem-aws-s3-v2 (Allows you to use S3 storage with AWS SDK v2)
league/flysystem suggests installing league/flysystem-aws-s3-v3 (Allows you to use S3 storage with AWS SDK v3)
league/flysystem suggests installing league/flysystem-azure (Allows you to use Windows Azure Blob storage)
league/flysystem suggests installing league/flysystem-cached-adapter (Flysystem adapter decorator for metadata caching)
league/flysystem suggests installing league/flysystem-eventable-filesystem (Allows you to use EventableFilesystem)
league/flysystem suggests installing league/flysystem-rackspace (Allows you to use Rackspace Cloud Files)
league/flysystem suggests installing league/flysystem-sftp (Allows you to use SFTP server storage via phpseclib)
league/flysystem suggests installing league/flysystem-webdav (Allows you to use WebDAV storage)
league/flysystem suggests installing league/flysystem-ziparchive (Allows you to use ZipArchive adapter)
league/flysystem suggests installing spatie/flysystem-dropbox (Allows you to use Dropbox storage)
league/flysystem suggests installing srmklive/flysystem-dropbox-v2 (Allows you to use Dropbox storage for PHP 5 applications)
laravel/framework suggests installing aws/aws-sdk-php (Required to use the SQS queue driver and SES mail driver (~3.0).)
laravel/framework suggests installing doctrine/dbal (Required to rename columns and drop SQLite columns (~2.6).)
laravel/framework suggests installing ext-pcntl (Required to use all features of the queue worker.)
laravel/framework suggests installing ext-posix (Required to use all features of the queue worker.)
laravel/framework suggests installing guzzlehttp/guzzle (Required to use the Mailgun and Mandrill mail drivers and the ping methods on schedules (~6.0).)
laravel/framework suggests installing league/flysystem-aws-s3-v3 (Required to use the Flysystem S3 driver (~1.0).)
laravel/framework suggests installing league/flysystem-cached-adapter (Required to use the Flysystem cache (~1.0).)
laravel/framework suggests installing league/flysystem-rackspace (Required to use the Flysystem Rackspace driver (~1.0).)
laravel/framework suggests installing league/flysystem-sftp (Required to use the Flysystem SFTP driver (~1.0).)
laravel/framework suggests installing nexmo/client (Required to use the Nexmo transport (~1.0).)
laravel/framework suggests installing pda/pheanstalk (Required to use the beanstalk queue driver (~3.0).)
laravel/framework suggests installing predis/predis (Required to use the redis cache and queue drivers (~1.0).)
laravel/framework suggests installing pusher/pusher-php-server (Required to use the Pusher broadcast driver (~3.0).)
laravel/framework suggests installing symfony/dom-crawler (Required to use most of the crawler integration testing tools (~4.0).)
laravel/framework suggests installing symfony/psr-http-message-bridge (Required to psr7 bridging features (~1.0).)
psy/psysh suggests installing ext-pcntl (Enabling the PCNTL extension makes PsySH a lot happier :))
psy/psysh suggests installing ext-posix (If you have PCNTL, you'll want the POSIX extension as well.)
psy/psysh suggests installing ext-pdo-sqlite (The doc command requires SQLite to work.)
psy/psysh suggests installing hoa/console (A pure PHP readline implementation. You'll want this if your PHP install doesn't already support readline or libedit.)
filp/whoops suggests installing whoops/soap (Formats errors as SOAP responses)
sebastian/global-state suggests installing ext-uopz (*)
phpunit/php-code-coverage suggests installing ext-xdebug (^2.6.0)
phpunit/phpunit suggests installing phpunit/php-invoker (^2.0)
phpunit/phpunit suggests installing ext-soap (*)
phpunit/phpunit suggests installing ext-xdebug (*)
Writing lock file
Generating optimized autoload files
> Illuminate\Foundation\ComposerScripts::postAutoloadDump
> @php artisan package:discover
Discovered Package: fideloper/proxy
Discovered Package: laravel/tinker
Discovered Package: nunomaduro/collision
Package manifest generated successfully.
> @php artisan key:generate
Application key [base64:FA5PvB7bGHRAeuBn5o4Juv6ls0xSzs8RVWhpLiiAi9c=] set successfully.
Fri Jun  8 00:32:20 UTC 2018
```

From `Fri Jun  8 00:30:02 UTC 2018` to `Fri Jun  8 00:32:20 UTC 2018`


