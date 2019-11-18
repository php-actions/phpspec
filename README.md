<img src="http://52.48.57.141/php-actions.png" align="right" alt="PHP Actions for Github" />

Run your phpspec tests in your Github Actions.
==============================================

phpspec is a tool which can help you write clean and working PHP code using behaviour driven development or BDD. BDD is a technique derived from test-first development.

Usage
-----

Create your Github Workflow configuration in `.github/workflows/ci.yml` or similar.

```yaml
name: CI

on: [push]

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
    - uses: actions/checkout@v1
    - uses: php-actions/composer@master # or alternative dependency management
    - name: phpspec
      uses: php-actions/phpspec@master
      with:
        config: phpspec.yml # or wherever your config file is
    # ... then your own project steps ...
```

Example with matrix
-------------------
```yaml
name: CI

on: [push]

jobs:
  build:
    name: PHP ${{ matrix.php }} (${{ matrix.os }})

    runs-on: ${{ matrix.os }}

    strategy:
      fail-fast: false
      matrix:
        php: [ 7.1, 7.2, 7.3, 7.4, nightly ]
        os: [ ubuntu-latest ]

    steps:
    - name: Checkout
      uses: actions/checkout@master

    - name: Setup PHP
      uses: shivammathur/setup-php@master
      with:
        php-version: ${{ matrix.php }}

    - uses: php-actions/composer@master

    - name: PHP spec
      uses: php-actions/phpspec@master
      with:
        config: phpspec.yml
```
