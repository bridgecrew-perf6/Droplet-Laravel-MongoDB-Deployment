<h1>Deploying a Laravel and MongoDB project on a Digital Ocean Droplet</h1>

Go to marketplace when setting up your droplet and select the Laravel image
<h2>Commands I used</h2>
<h3>Connect</h3>
ssh root@'ip_of_droplet' <br>

<h3>Unistall Nginx</h3>
sudo apt-get purge nginx nginx-common   <br>
sudo apt-get update   <br>
sudo apt-get install apache2<br>

<h3>Install apache2</h3>
sudo apt-get install libapache2-mod-php7.4 <br>
sudo service apache2 restart <br>

<h3>Install perl -> install mongodb later</h3>
sudo apt-get install php7.x-dev		Install pecl to install mongodb<br>

<h3>Install npm</h3>
sudo apt update<br>
sudo apt install nodejs<br>
sudo apt install npm<br>

<h3>Install mongodb</h3>
https://www.digitalocean.com/community/tutorials/how-to-install-mongodb-on-ubuntu-18-04-source<br>

sudo pecl install mongodb<br>
echo "extension=mongodb.so" >> /etc/php/7.4/cli/php.ini <br>

<h3>Upload project</h3>
git clone https://github.com/<project><br>

<h3>Install packages</h3>
composer install<br>
npm install<br>

<h3>Set up .env and app key -> very important</h3>
cp .env.example .env<br>
nano .env<br>
php artisan key:generate<br>

<h3>Set permissions</h3>
sudo chmod 0777 -R <project><br>
sudo chmod 0777 -R storage<br>

<h3>Migrate database</h3>
php artisan migrate<br>

<h3>Change document root</h3>
nano /etc/apache2/sites-available/000-default.conf<br>

Change DocumentRoot -> "DocumentRoot = <location of public folder in project>"<br>
<Directory "path/to/laravel/project/public"><br>
    Allowoverride All<br>
\</Directory><br>

sudo a2enmod rewrite	In project directory<br>

sudo service apache2 restart <br>

<h3>To set up swap memory</h3>
https://www.digitalocean.com/community/tutorials/how-to-add-swap-space-on-ubuntu-18-04
