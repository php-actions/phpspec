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
    - uses: phpactions/composer@master # or alternative dependency management
    - name: phpspec
      uses: phpactions/phpspec@master
      with:
        config: phpspec.yml # or wherever your config file is
    # ... then your own project steps ...
```