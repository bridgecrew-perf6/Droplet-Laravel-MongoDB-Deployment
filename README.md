#Deploying a Laravel and MongoDB project on a Digital Ocean Droplet

Go to marketplace when setting up your droplet and select the Laravel image
#Commands I used
##Connect
ssh root@<ip_of_droplet>

##Unistall Nginx
sudo apt-get purge nginx nginx-common  
sudo apt-get update  
sudo apt-get install apache2

##Install apache2
sudo apt-get install libapache2-mod-php7.4 
sudo service apache2 restart 

##Install perl -> install mongodb later
sudo apt-get install php7.x-dev		Install pecl to install mongodb

##Install npm
sudo apt update
sudo apt install nodejs
sudo apt install npm

##Install mongodb
https://www.digitalocean.com/community/tutorials/how-to-install-mongodb-on-ubuntu-18-04-source

sudo pecl install mongodb
echo "extension=mongodb.so" >> /etc/php/7.4/cli/php.ini 

##Upload project
git clone https://github.com/<project>

##Install packages
composer install
npm install

##Set up .env and app key -> very important
cp .env.example .env
nano .env
php artisan key:generate

##Set permissions
sudo chmod 0777 -R <project>
sudo chmod 0777 -R storage

##Migrate database
php artisan migrate

##Change document root
nano /etc/apache2/sites-available/000-default.conf
"
Changed DocumentRoot
<Directory "path/to/laravel/project/public">
    Allowoverride All
</Directory>"

sudo a2enmod rewrite	In project directory

sudo service apache2 restart 

##To set up swap memory
https://www.digitalocean.com/community/tutorials/how-to-add-swap-space-on-ubuntu-18-04
