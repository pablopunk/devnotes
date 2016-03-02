
# Working Copy installation

## Requirements

### apache, php and mysql
Download [MAMP](https://www.mamp.info/en/) or install them separately
### git
```bash
brew install git # Mac OS X
sudo apt-get install -y git # Ubuntu
```
### composer
```bash
curl -sS https://getcomposer.org/installer | php # install on directory
sudo mv composer.phar /usr/local/bin/composer # move to bin
sudo chmod 755 /usr/local/bin/composer
```
### nodejs
Download [from web](https://nodejs.org/en/)

### bower
```bash
npm install bower -g
```

## Configure

Clone the repo
```bash
git clone https://stang-decision-systems.git.beanstalkapp.com/stang.git && cd stang
```
Add a file `app/config/parameters.yml` with your config:
```json
parameters:
        database_driver: pdo_mysql
        database_host: 127.0.0.1
        database_port: "8889"
        database_name: stangs_dev
        database_user: root
        database_password: root
        mailer_transport: smtp
        mailer_host: 127.0.0.1
        mailer_user: null
        mailer_password: null
        locale: en
        secret: ThisTokenIsNotSoSecretChangeIt
        installation_name: "Pablo Working Copy"
        installation_id: "server"
        nskey: asDDduf9an3mSa8yudf0kqpm14ei8737yaz0oKKcxg1hm487dfh289nSDsde1r
        installation_key: 7zcCOs51J9yivFplm5mt
        keysurvey_login: "spencer@sportlabinc.com"
        keysurvey_password: "Bi11ieBean!"
        router.request_context.base_url: "/stang"
```

Install dependencies
```bash
composer install
bower install
php app/console cache:clear -e prod
```

- If the "php cache:clear" command **fails with an error** related to `date.timezone` use this command (with your location and file)
```bash
echo "date.timezone = Europe/Madrid" >> path/to/your/php.ini
```

- If the error was `non-existent service "assets.packages"` install this:
```bash
composer require stfalcon/tinymce-bundle:0.3.9
```

If this dependency didn't exist in the composer.json, you can remove it now **from that file** (as it's already installed).

Now let's flash the database. First create an empty database using the user/password you have in your `app/config/parameters.yml` and using that database_name

```bash
$ mysql -u root -p
mysql> create database stangs_dev;
```

Download the database from the server (be sure you have credentials)

```bash
$ php app/console database:flash
Remote Server Domain or IP: 67.225.129.42
Remote Server User: diego
Remote Server Password:
Remote Server Database Name: diego_stangsdb
```

This takes a while. If it downloaded the .sql script at `/tmp` but *it failed* installing locally you can do it manually
```bash
$ mysql -u root -p
mysql> use stangs_dev;
mysql> source /path/to/script.sql
```

After some minutes the db should be installed

Now edit these `/php.core` lines 35-39 to your own working copy:
```php
} else if(gethostname() == 'Retinilla.local' || gethostname() == 'Retinilla' || gethostname() == '127.0.0.1' || gethostname() == 'localhost'){ // Pablo's working copy
    // Pablo Dev
    $prefix = dirname(__FILE__);
    $root1 = '/Users/punks/mamp';
    $root2 = 'localhost:80';
```

It should be working now. Open a browser with your local server path [http://localhost/stang](``http://localhost/stang``).

If you get an error or nothing happens clear the cache with ``php app/console cache:clear -e prod`` or change the project to "developer mode" for error details ``touch .dev #creates a hidden file``

Under **linux** php is not usually configured to use the default `short_open_tag` so you may have errors related to this. Just edit your `php.ini` and change the value to On
```bash
short_open_tag = Off # before
short_open_tag = On  # after
```
