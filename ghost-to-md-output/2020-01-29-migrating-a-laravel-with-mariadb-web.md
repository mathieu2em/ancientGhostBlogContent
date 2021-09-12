---
title: Migrating An Existing Laravel/MariaDB Project On A New System From Scratch.
slug: migrating-a-laravel-with-mariadb-web
date_published: 2020-01-30T01:37:27.000Z
date_updated: 2021-01-11T01:18:54.000Z
tags: database, webapp, Laravel, mariaDB
excerpt: I recently had to migrate a laravel web app using mariadb on my computer to setup a test and development environment.I will tell you the steps I went through and the difficulties that happened as well as the solutions I used to solve it. 
---

I recently had to migrate a laravel web app using mariadb on my computer to setup a test and development environment.

I will tell you the steps I went through and the difficulties that happened as well as the solutions I used to solve it. 

## making sure my fresh linux mint system is ready

so to be able to use laravel I started by searching on the web how to install it on my machine which is running linux mint 19.1 with XFCE.

I used [this page](https://www.howtoforge.com/tutorial/install-laravel-on-ubuntu-for-apache/) from [Christophe Jossart](https://medium.com/@colorfield) to do so. I will tell you the same he did for this part.

first, let's do the habitual update/upgrade stuff:

`sudo apt-get update`
`sudo apt-get upgrade`

> "Next step is to install PHP along with several extra packages that would prove useful if you are going to work with Laravel."

    sudo add-apt-repository ppa:ondrej/php
    sudo apt-get update
    sudo apt-get install apache2 libapache2-mod-php7.2 php7.2 php7.2-xml php7.2-gd php7.2-opcache php7.2-mbstring

this installs php with severa extra packages
now we want to be able to use composer in our system. Composer being a dependency manager for php ([see more here](https://getcomposer.org/))

just as Mr Jossart said "The curl command downloads composer.phar package to your /tmp directory.  But we would want composer to run globally hence we need to move it to */usr/local/bin/* directory under the name '*composer*'. Now we can run composer from anywhere."

    cd /tmp
    curl -sS https://getcomposer.org/installer | php
    sudo mv composer.phar /usr/local/bin/composer

now this part install composer and makes it usable in our entire system.
We now thank Mr Jossart for his help and follow up with another person. Him was gonna setup a new laravel system. But WE already have a repository with a laravel webapp on github. Hence we will not have to do everything from scratch. We will 

1. go on our repository
2. clone our repository in our system using  `git clone theRepoAddress` to do so.
3. we will cd in the directory of our freshly cloned repo. `cd theRepoDir`

### installing MariaDB mysql 

We now have to install MariaDB and mysql. To do so, I used [this page](https://linuxize.com/post/how-to-install-mariadb-on-ubuntu-18-04/). Which makes it pretty simple because you only have to use this command: 

    sudo apt install mariadb-server

the command to install mariadb
> The MariaDB service will start automatically. You can verify it by typing:

    sudo systemctl status mariadb

        ● mariadb.service - MariaDB database server
    Loaded: loaded (/lib/systemd/system/mariadb.service; enabled; vendor preset
    Active: active (running) since Sun 2018-07-29 19:31:31 UTC; 38s ago
    Main PID: 13932 (mysqld)
    Status: "Taking your SQL requests now..."
        Tasks: 27 (limit: 507)
    CGroup: /system.slice/mariadb.service
            └─13932 /usr/sbin/mysqld

output
Now, here comes some fun. We want to have our own .env file so our laravel web app knows where to search for what. So we will create a mysql user and password as well as a database. To do so I used the help of [this page](http://www.daniloaz.com/en/how-to-create-a-user-in-mysql-mariadb-and-grant-permissions-on-a-specific-database/).

> we want to enter in the mysql repl as root : `sudo mysql -u root -p`

> now we want to create a new user. Be sure to replace MyUsername and MyPassword with your own chosen username and password : 

    CREATE USER 'MyUsername' IDENTIFIED BY 'MyPassword';

> now we want to create the database (change DBname for the name you want for your database) : `CREATE DATABASE `DBname`;`

> now lets grant permissions :

    GRANT USAGE ON *.* TO 'myuser'@localhost IDENTIFIED BY 'mypassword';

    GRANT ALL privileges ON `theDatabaseYouCreated`.* TO 'theUserYouCreated'@localhost;

> Apply changes made

> To be effective the new assigned permissions you must finish with the following command:

    FLUSH PRIVILEGES;

> now we get out of mysql with this command : `\q`

### Setting the .env file of our laravel project

first of all be sure to be at the root of your laravel project directory.

good. Now there is always a file named .env.example copy it to .env like this in your terminal: `cp .env.example .env`

now open it with you favorite text editor and enter the username, password and database name you chose in the last step in these three columns:

    DB_DATABASE=putTheDBNameHere
    DB_USERNAME=putYourUsernameHere
    DB_PASSWORD=putYourPasswordHere

now be sure that you are in you repo file and do this command

    composer install

now you should be good to do the following command which will migrate the laravel webapp for you : 

`php artisan migrate:fresh --seed`

> *for me, it didnt work as it gave me this error : *

> *Symfony\Component\Debug\Exception\FatalErrorException  : Trait 'App\Providers\Illuminate\Support\Facades\Schema' not found*

> I fixed it by installing this package

> `sudo apt-get install php7.2-mysql`

> if your php version is different you can verify it with php --version and then install the concording php-mysql package.

> I then faced this probleme: 

> Illuminate\Database\QueryException  : SQLSTATE[42000]: Syntax error or access violation: 1071 Specified key was too long; max key length is 767 bytes (SQL: alter table `users` add unique `users_username_unique`(`username`))

> which is something with the charTypes. I fixed it by going in my AppServiceProvider.php file located in myLaravelProjectDir/app/Providers/

> and added in the boot function `Schema::defaultStringLength(191);`

        public function boot()
        {
            //
            \Schema::defaultStringLength(191);
        }

the function is already there . just add the Schema line to it
**you can now migrade the Jobs to your local system individually using : **

`php artisan job:dispatch JOB1 JOB2 ...`

then generate a key from artisan to be able to launch your test server with

     php artisan key:generate

then you can launch the server with serve

     php artisan serve

other resource I used:
[

Install an existing Laravel project

Check if the values in config/app.php meets your needs, depending where (staging, dev, …) and how (php -S, artisan, vm with a domain, …) you are running it. Time to check your site, depending on…

![](https://cdn-images-1.medium.com/fit/c/152/152/1*8I-HPL0bfoIzGied-dzOvA.png)Christophe JossartMedium

![](https://miro.medium.com/proxy/1*3sela1OADrJr7dJk_CXaEQ.png)
](https://medium.com/@colorfield/install-an-existing-laravel-project-c6e6bf28d5c6)
blog post banner attribution : [People vector created by pch.vector - www.freepik.com](https://www.freepik.com/vectors/people)
