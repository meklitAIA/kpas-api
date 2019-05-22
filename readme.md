### Requirements

* PHP version >= 7.2
* 1 MySQL database (version >= 5.7) or MariaDB (version >= 10.0)
* 1 SMTP e-mail account
* Disk space at least 1 GB and external disk for users' files

### Technologies

* PHP 7.2 or newer
* Laravel 5.8 or newer
* MySQL 5.7 or newer / MariaDB 10 or newer

### Installation

To install project on new server, please perform actions in following order:

```$xslt
# Generate SSH key
$ ssh-keygen -t rsa -b 4096 -C "{email}"

# Copy content of file `.ssh/id_ras.pub` and add new deploy key to project's repository on GitHub (`Settings > Deploy keys`).

# Clone repository on server
$ git init
$ git remote add origin git@github.com:{user}/{repo}.git
$ git pull origin {branch}

# Download PHP dependencies
$ composer install (--no-dev when *{branch} = master*)

# Set environment
$ php artisan env:set {mode} (dev, production etc.)

# Run migrations & seeders

$ php artisan migrate --force
$ php artisan db:seed --force
$ php artisan passport:install

# Copy passport auth data from table oauth_clients to .env

PASSWORD_CLIENT_ID=
PASSWORD_CLIENT_SECRET=

# Set permissions (if user has not permissions to write):
$ chmod 0777 boostrap/cache
$ chmod 0777 storage

# Generate secret key
$ php artisan key:generate

```

### Update

```$xslt
# Please perform actions in following order
$ git pull origin {branch} (that same branch that was used during installation)
$ composer install (when composer.lock has changed)
$ php artisan migrate
$ php artisan db:seed
# *update `.env` file when necessary*
```
