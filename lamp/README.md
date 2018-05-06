# LAMP stacks with **xdebug** and **PHPunit**

Add xdebug and phpunit to the official php:7-apache image.


See [ECLIPSE.md](ECLIPSE.md) to configure Eclipse.  

See the [sample](sample/) code for a basic lamp stack.

## Requirement

- Eclipse PDT
- docker
- docker-compose

## Start server
```bash
cd sample/
docker-compose up
# press Ctrl+c to stop
```
## Debug app

- Run Eclipse debugger
- Open any url from your browser

## Debug tests

- Run Eclipse debugger
- Run PHPUnit :
    - Using a bash session
        ```bash
        # Start a bash session
        docker exec -it <CONTAINER_ID> bash 
        # Automaticly run tests on files changes
        watch-phpunit -c specs/suite.xml
        # Use PHPUnit cli
        phpunit --bootstrap specs/autoload.php specs/tests/
        ```
    - Using docker exec
        ```bash
        # Automaticly run tests on files changes
        docker exec -it <CONTAINER_ID> watch-phpunit -c specs/suite.xml
        # Use PHPUnit cli
        docker exec -it <CONTAINER_ID> phpunit --bootstrap specs/autoload.php specs/tests/
        ```

## Live reload PhpUnit

```bash
watch-phpunit [-c <config> | -b <bootstrap> -f <file>] [-w <dir-or-file-to-watch> default:/var/www/html]
    # Examples
    watch-phpunit -b autoload.php -f specs/tests/MyTest.php
    watch-phpunit -c suite.xml
    watch-phpunit -c suite.xml -w index.php
    watch-phpunit -c suite.xml -w specs/tests
```

