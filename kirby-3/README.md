# Docker Basic Nginx and PHP
- php-fpm 8 alpine (preinstallation of all basic packages out of the box)
- nginx apline incl php-fpm configuration

## TODOs
- define your user ID on local machine (ideally no `root`) and put it into .env file (otherwise, your content will not be accessible in the FE due to the rights)
- Symlink your project git `ln -s /path/to/your/git/docroot htdocs`

## Hints
- work with composer inside of docker container