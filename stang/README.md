
# Working Copy installation

## Requirements

### apache, php and mysql
Download [MAMP](https://www.mamp.info/en/) or install the separately
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

If the "php cache:clear" command **fails with error** `non-existent service "assets.packages"` install this:

```bash
composer require stfalcon/tinymce-bundle:0.3.9
```

If this dependency didn't exist in the composer.json, you can remove it now **from that file** (as it's already installed).

Now edit these `/php.core` lines 35-39 to your own working copy:
```php
} else if(gethostname() == 'Retinilla.local' || gethostname() == 'Retinilla' || gethostname() == '127.0.0.1' || gethostname() == 'localhost'){ // Pablo's working copy
    // Pablo Dev
    $prefix = dirname(__FILE__);
    $root1 = '/Users/punks/mamp';
    $root2 = 'localhost:80';
```

Finally change the project "developer mode" if you want
```bash
touch .dev
```
