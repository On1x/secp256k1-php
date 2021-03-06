# secp256k1-php

[![Build Status](https://travis-ci.org/Bit-Wasp/secp256k1-php.svg?branch=master)](https://travis-ci.org/Bit-Wasp/secp256k1-php)
[![codecov](https://codecov.io/gh/Bit-Wasp/secp256k1-php/branch/master/graph/badge.svg)](https://codecov.io/gh/Bit-Wasp/secp256k1-php)

PHP bindings for https://github.com/bitcoin-core/secp256k1

Please note that the upstream library, [libsecp256k1](https://github.com/bitcoin-core/secp256k1) is still considered
experimental by it's authors, and has not yet been formally released. For this reason, it's use should be
discouraged. For consensus systems this warning is critical.

The library supports the EcDH, and signature recovery modules - these libraries are required for installation.

### Requirements
PHP 5.* versions are supported in the v0.0.x release.
PHP 7 is supported in the v0.1.x series.

### About the extension
  - Fully unit tested, with >99 code coverage since the v0.1.3 release.
  - This extension only supports deterministic signatures at present. In fact, no RNG is utilized in this extension - private keys must be generated elsewhere.
  - The extension exposes the same raw API of libsecp256k1. As such, you must ensure you are passing the binary representations of each value.
  - In keeping with libsecp256k1, this extension returns certain data to the user by writing to a variable reference, and returning a code indicating the failure/success.

### Fast install for PHP7
```
mkdir php-ext-secp256k1
cd php-ext-secp256k1

git clone https://github.com/bitcoin-core/secp256k1 && \
cd secp256k1 && \
git checkout 95e99f196fd08a8b2c236ab99d7e7fec8f6dc78f
./autogen.sh && \
./configure --enable-experimental --enable-module-ecdh --enable-module-recovery && \
make && \
make install 

cd .. && \
git clone https://github.com/Bit-Wasp/secp256k1-php.git && \
cd secp256k1-php && \
cd secp256k1 && \
phpize && \
./configure --with-secp256k1 && \
make && \
make install
```

### To Install:

libsecp256k1:
```
    git clone https://github.com/bitcoin-core/secp256k1 && \
    cd secp256k1 &&                                    \
    ./autogen.sh &&                                    \
    ./configure --enable-experimental --enable-module-ecdh --enable-module-recovery && \
     make &&                                           \
     sudo make install &&                              \
     cd ../
```

secp256k1-php:
```
    git clone https://github.com/On1x/secp256k1-php && \
    cd secp256k1-php/secp256k1 &&                      \
    phpize &&                                          \
    ./configure --with-secp256k1 &&                    \
    make && sudo make install &&                       \
    cd ../../
```

### Examples

See [the examples folder](./examples), or [the *_basic.phpt files in the test suite](./secp256k1/tests)
### (Optional) - Enable extension by default!
If you're a heavy user, you can add this line to your php.ini files for php-cli, apache2, or php-fpm.
> /etc/php/7.0/cli/conf.d/20-secp256k1.ini -> /etc/php/7.0/mods-available/secp256k1.ini
> echo "extension=secp256k1.so" >> /etc/php/7.1/fpm/php.ini
```
extension=secp256k1.so
```

### Run Tests

(Commands issued from secp256k1-php directory)

Basic tests:

    cd secp256k1-php/secp256k1 && make test

Data fixture tests (requires composer install):

    cd secp256k1-php && \
    composer install && \ # required the first time only
    php -dextension=secp256k1.so vendor/bin/phpunit tests/
