
<img src="img/button-bubble-info.png"/>

# Info
## Introduction
>"_Kids, by the time you're grown there are some things I want you to learn about.  Here is a list._"
-This Guy.

In This Document

[Getting Started](#getting-started)

[macOS Development](#macos-development)

[Android Development](#android-development)

[Android Studio](#android-studio)

[Webserver Development](#webserver-development)

[Linux Stuff](#linux-stuff)

[Sublime Text](#sublime-text)

## Getting Started
>"_Make sure that you know how to use the console or command-prompt on your computer_"
-Same Guy

- Mac
    + Terminal
        * shortcut: <kbd>command</kbd>+<kbd>space</kbd> and type `terminal`
- PC
    + Power Shell
        * shortcut: <kbd>Windows</kbd>+<kbd>X</kbd> and type <kbd>A</kbd>

## macOS Development

- View all files in `Finder` 
    + <kbd>shift</kbd>+<kbd>command</kbd>+<kbd>.</kbd>
- Print Working Directory
```shell
$ pwd
```

- Output log of all macOS downloaded content
```shell
$ sqlite3 ~/Library/Preferences/com.apple.LaunchServices.QuarantineEventsV* 'select LSQuarantineDataURLString from LSQuarantineEvent'
```

- Remove log of all macOS downloaded content
```shell
$ sqlite3 ~/Library/Preferences/com.apple.LaunchServices.QuarantineEventsV* 'delete from LSQuarantineEvent'
```

- Install [Homebrew](https://brew.sh), the macOS package manager
```shell
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

- Elevate to root
```shell
$ sudo bash
Password:🗝
```

- Copy contents of i`d_rsa.pub` file to your clipboard
```shell
$ pbcopy < ~/.ssh/id_rsa.pub
```

## Android Development
> "_Be aware the subtle nuances between pure Android development and Samsung Android dev_."
-🧚

- Reboot Android device to bootloader
```shell
$ adb reboot bootloader
```

- Reboot Android device to fastboot (*non-Samsung*)
```shell
$ adb reboot fastboot
```

- Wipe Android device's User data (_Cracked screen, need to wipe?_)
```shell
$ adb fastboot -w
```

- OEM Unlock Android device bootloader
```shell
$ fastboot oem unlock
```

- Flash the bootloader partition with the file dragged into the console window
```shell
$ fastboot flash bootloder 
```

- Erase Dalvik cache
```shell
$ fastboot erase cache
```

- Reboot Android device (from Fastboot)
```shell
$ fastboot reboot
```

### Android Studio
- Enable keyboard input without editing the `config.ini`:

Tools → Android → AVD Manager →✏️→ Show Advanced Settings (scroll to bottom) → Enable Keyboard Input

## Webserver Development
- Install packages necessary to host webpages
```shell
$ sudo apt-get install php5 apache2 libapache2-mod-php5 php5-curl libapache2-mod-auth-mysql mysql-server php5-mysql phpmyadmin
```

- Setup MySQL
- 
```shell
$ mysql_secure_installation
$ mysql -u root -p
```

- Enable Apache2 rewrite module
```shell
$ a2enmod rewrite
```

- Enable headers rewrite module
```shell
$ a2enmod headers
```

- Enable mcrypt
```shell
$ sudo php5enmod mcrypt
```

- Restart Apache
```shell
$ sudo service apache2 restart
```

- Install Remote Sublime Text Binary
```shell
$ sudo wget -O /usr/local/bin/rmate https://raw.github.com/aurora/rmate/master/rmate
$ sudo chmod a+x /usr/local/bin/rmate
```

- Edit `mysql` config
```shell
$ rmate /etc/mysql/my.cnf
```

- Enable `mysqli`
```shell
$ rmate /etc/php/7.0/apache2/php.ini
```

- Make `phpMyAdmin` viewable
```shell
sudo ln -s /usr/share/phpmyadmin /var/www/html/phpmyadmin

```

- **Edit Apache Configuration**
```shell
$ rmate /etc/apache2/apache2.conf
```

- **View Apache Error Log**
```shell
$ rmate /var/log/apache2/error.log
```

- Update `cURL`
```shell
$ ! /usr/bin/env bash
```

- Install any build-dependencies necessary for `cURL`
```shell
$ sudo apt-get build-dep curl
```

- Get latest `libcurl` (as of: **Feb 25, 2016**)
```shell
$ mkdir ~/curl
$ cd ~/curl
$ wget http://curl.haxx.se/download/curl-7.50.2.tar.bz2
$ tar -xvjf curl-7.50.2.tar.bz2
$ cd curl-7.50.2
```
    ...build from source
```shell
$ ./configure
$ ./make
$ sudo make install
```

- Update `SSL` (Avoid **Heart Bleed**)
```shell
$ sudo apt-get install make (Install compiling library Make)
$ wget https://www.openssl.org/source/openssl-1.0.2g.tar.gz
$ tar -xzvf openssl-1.0.2g.tar.gz
$ cd openssl-1.0.2g
$ sudo ./config
$ sudo make install
$ sudo ln -sf /usr/local/ssl/bin/openssl `which openssl`
$ openssl version -v
```

>_In Review_: Symbolic Link `ln -s` [current-target] [new-location]

- Allow `Access-Control` to share Font cross-site
- Edit Apache2 Configuration:
```shell
<FilesMatch "\.(ttf|otf|eot|woff)$">
  <IfModule mod_headers.c>
    Header set Access-Control-Allow-Origin "*"
  </IfModule>
</FilesMatch>
```

- **SSL Certificates** with _Let's Encrypt_
    + First, add the repository:
    ```shell
    $ sudo add-apt-repository ppa:certbot/certbot
    ```
    + press <kbd>enter</kbd> to accept.  Next, update the package and install
    ```shell
    $ sudo apt-get update && sudo apt-get install python-certbot-apache
    ```
    + Generate SSL Certificate
```shell
$ certbot-auto --apache certonly -d domain.com -d www.domain.com -d sub1.domain.com -d sub2.domain.com -d sub2.domain.com
```

- Remove a _Let's Encrypt_ SSL Certificate

```shell
$ rm -rf /etc/letsencrypt/archive/domain.com/
$ rm -rf /etc/letsencrypt/live/domain.com/
$ rm -rf /etc/letsencrypt/renewal/domain.com.conf
```

- Edit SSL Certificate configuration
```shell
$ rmate /etc/apache2/sites-available/000-default-le-ssl.conf
```

- Set up Auto-Renewal
To run the renewal check daily, we will use `cron`, a standard system service for running periodic jobs. We tell `cron` what to do by opening and editing a file called a `crontab`
```shell
$ sudo crontab -e
```

Your text editor will open the default crontab which is a text file with some help text in it. Paste in the following line at the end of the file, then save and close it:
```shell
. . .
15 3 * * * /usr/bin/certbot renew --quiet
```
The `15 3 * * *` part of this line means "run the following command at 3:15 am, every day". You may choose any time.

The `renew` command for Certbot will check all certificates installed on the system and update any that are set to expire in less than thirty days. `--quiet` tells Certbot not to output information nor wait for user input.

`cron` will now run this command daily. Because we installed our certificates using the `--apache` plugin, Apache will also be reloaded to ensure the new certificates are used.

## Linux Stuff
+ Shortcuts
    * `id username` 
        - List primary and secondary groups for `username` 
    * `ls ~` 
        - List contents of home directory

+ User Modification
    - Add a `username` and assign secondary group: `tomcat7`
    ```shell
    $ sudo useradd -G tomcat7 -m username
    ```

    - Recursively delete user and /home directory
```shell
$ sudo userdel -r username
```

    - Assign primary group named `primarygroup` for user named `username`
```shell
$ sudo usermod -g primarygroup username
```

    - Modify the secondary group(s) (comma,delimited,list) of `username`
```shell
$ sudo usermod -G admin,adm,merchant,issuer,username username
```

    - Add a new group named `groupname`
```shell
$ sudo groupadd groupname
```

    - Recursively change the owner of file `directoryname` to `groupname`
```shell
$ sudo chgrp -R groupname directoryname
```

    - Change shell to bash (**bash history**) for `username`
```shell
$ sudo cash -s /bin/bash username
```
- BASH Aliases
    + Create/Edit `~/.bash_aliases`
    + Add:
        * `alias rsub='rmate $1'`
        * _no whitespace around '='_
    + Set permissions
    ```shell
    $ chmod a+x ~/.bash_aliases
    ```
    + Source `~/.bash_aliases` (Restart)
    ```shell
    $ source ~/.bash_aliases
    ```


## Sublime Text
- Open `.ssh/config` in Sublime Text locally
```shell
$ subl ~/.ssh/config
```

    + Add following to enable remote Sublime Text editting:
    ```shell
    Host domain.com
    RemoteForward 52698 127.0.0.1:52698
    ```
