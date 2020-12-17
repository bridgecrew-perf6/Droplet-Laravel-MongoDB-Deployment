<h1>Deploying a Laravel and MongoDB project on a Digital Ocean Droplet</h1>

Go to marketplace when setting up your droplet and select the Laravel image
<h2>Commands I used</h2>
<h3>Connect</h3>
ssh root@<ip_of_droplet>

<h3>Unistall Nginx</h3>
sudo apt-get purge nginx nginx-common  
sudo apt-get update  
sudo apt-get install apache2

<h3>Install apache2</h3>
sudo apt-get install libapache2-mod-php7.4 
sudo service apache2 restart 

<h3>Install perl -> install mongodb later</h3>
sudo apt-get install php7.x-dev		Install pecl to install mongodb

<h3>Install npm</h3>
sudo apt update
sudo apt install nodejs
sudo apt install npm

<h3>Install mongodb</h3>
https://www.digitalocean.com/community/tutorials/how-to-install-mongodb-on-ubuntu-18-04-source

sudo pecl install mongodb
echo "extension=mongodb.so" >> /etc/php/7.4/cli/php.ini 

<h3>Upload project</h3>
git clone https://github.com/<project>

<h3>Install packages</h3>
composer install
npm install

<h3>Set up .env and app key -> very important</h3>
cp .env.example .env
nano .env
php artisan key:generate

<h3>Set permissions</h3>
sudo chmod 0777 -R <project>
sudo chmod 0777 -R storage

<h3>Migrate database</h3>
php artisan migrate

<h3>Change document root</h3>
nano /etc/apache2/sites-available/000-default.conf
"
Changed DocumentRoot
<Directory "path/to/laravel/project/public">
    Allowoverride All
</Directory>"

sudo a2enmod rewrite	In project directory

sudo service apache2 restart 

<h3>To set up swap memory</h3>
https://www.digitalocean.com/community/tutorials/how-to-add-swap-space-on-ubuntu-18-04
