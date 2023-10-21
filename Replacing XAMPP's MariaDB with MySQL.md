# Replacing XAMPP's MariaDB with MySQL

## Overview

XAMPP is a free and open source cross-platform web server solution stack developed by Apache Friends that is available for Microsoft Windows. It contains Apache HTTP Server, MariaDB database and interpreters for scripts written in PHP and Perl programming languages.

The goal of this document is to replace XAMPP's default database software from MariaDB to MySQL.

## Requirements

- Windows PC
- Latest [XAMPP](https://sourceforge.net/projects/xampp/files/XAMPP%20Windows/) for windows, get the latest `.zip` file from the download page.
- Latest [MySQL 8](https://dev.mysql.com/downloads/mysql/) for windows, get the latest `.zip` file from the download page.

## Setup

- Extract downloaded `XAMPP.zip` file to `C:\xampp` folder.
- Open up `C:\xampp` folder and double click on `setup_xampp.bat` file to initialize the xampp installation.
- Double click on `xampp-control.exe` to open up XAMPP's control panel.
- Once in XAMPP's control panel, start the Apache service and make sure that it runs without any errors displayed on the console below.
- Stop all services and close XAMPP if you are currently running it.
- Rename the folder `C:\xampp\mysql` to `C:\xampp\mariadb`, this is just to backup the existing database.
- Open up the downloaded `mysql.zip` file, and copy/extract its contents into `C:\xampp\mysql` folder.
- Create a new file `C:\xampp\mysql\bin\my.ini` and copy this content:
    ```
    [mysqld]
    # Set basedir to your installation path
    basedir=c:/xampp/mysql

    # Set datadir to the location of your data directory
    datadir=c:/xampp/mysql/data

    # Default: 128 MB
    # New: 1024 MB
    innodb_buffer_pool_size = 1024M

    # Default since MySQL 8: caching_sha2_password
    default_authentication_plugin=mysql_native_password

    [client]
    ssl-mode=DISABLED
    ```
- Once that is done, we have to initialize our mysql database. ***This is a very important step and should not be skipped.*** Open up a terminal and go to `C:\xampp\mysql\bin` folder.
    ```batch
    cd C:\xampp\mysql\bin
    ```
- Then copy this into the terminal:
    ```batch
    mysqld.exe --default-authentication-plugin=mysql_native_password --initialize-insecure --basedir=c:\xampp\mysql --datadir=c:\xampp\mysql\data
    ```
- If it has already done its thing, close the terminal, and open up `xampp-control.exe` and start the MySQL service.

## Source

This was taken inspiration from [Daniel Opitz - Blog | XAMPP - Replacing MariaDB with MySQL 8](https://odan.github.io/2019/11/17/xampp-replacing-mariadb-with-mysql-8.html), and we thank him for documenting this process.
