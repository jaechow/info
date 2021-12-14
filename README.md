<link rel="ICON" sizes="16x16 32x32" type="image/x-icon" href="img/button-bubble-info.png"/>
<p align="center"><img src="img/button-bubble-info.png"/></p>

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
[![Live Demo](https://img.shields.io/badge/demo-online-green.svg)](https://jaechow.github.io/info/)
![Contributions welcome](https://img.shields.io/badge/contributions-welcome-orange.svg)
[![GitHub Issues](https://img.shields.io/github/issues/jaechow/info.svg)](https://github.com/jaechow/info/issues)
[![License](https://img.shields.io/badge/license-MIT-blue.svg)](https://opensource.org/licenses/MIT)
[![Awesome](https://cdn.rawgit.com/sindresorhus/awesome/d7305f38d29fed78fa85652e3a63e154dd8e8829/media/badge.svg)](https://github.com/sindresorhus/awesome)
<a href="https://twitter.com/intent/tweet?text=Check out this awesome README&url=https%3A%2F%2Fgithub.com%2Fjaechow%2Finfo">
<img src="https://img.shields.io/twitter/url/https/github.com/jaechow/info.svg?style=flat-square&logo=twitter" alt="GitHub tweet">
</a>

<p align="center">
    <a href="#windows-development">Windows Development</a> •
    <a href="#macos-development">macOS Development</a> •
    <a href="#android-development">Android Development</a> •
    <a href="#android-studio">Android Studio</a> •
    <a href="#webserver-development">Webserver Development</a> •
    <a href="#linux-stuff">Linux Stuff</a> •
    <a href="#sublime-text">Sublime Text</a> •
    <a href="#github-custom-emotes">GitHub Emotes</a>
</p>

# Info

## Introduction

>The living, breathing cheat-sheet!

## Windows Development

- Open the Power Shell prompt
    - shortcut: <kbd>Windows</kbd>+<kbd>X</kbd> and type <kbd>A</kbd>

- Install Chocolatey the Package Manager
>Run `Get-ExecutionPolicy`. If it returns `Restricted`, then run 
>`Set-ExecutionPolicy AllSigned` or `Set-ExecutionPolicy Bypass -Scope Process`.

```console
Set-ExecutionPolicy Bypass -Scope Process -Force; [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://community.chocolatey.org/install.ps1'))
```

- Enable GPG signing with native Windows Git

```console
foo@bar:~$ where gpg
C:\Program Files (x86)\GnuPG\bin\gpg.exe

foo@bar:~$ git config --global gpg.program "C:\Program Files (x86)\GnuPG\bin\gpg.exe"
```

## macOS Development

- Open the Terminal Emulator
    - * shortcut: <kbd>command</kbd>+<kbd>space</kbd> and type `terminal`
    - <kbd>command</kbd> is also <kbd>⌘</kbd>
    - <kbd>option</kbd> is also <kbd>⌥</kbd>
    - <kbd>control</kbd> is also <kbd>⌃</kbd>
    - <kbd>shift</kbd> is also <kbd>⇧</kbd>

- View all (hidden) files in Finder
    + <kbd>shift</kbd>+<kbd>command</kbd>+<kbd>.</kbd>
- Go To Folder (open system directory in Finder)
    + <kbd>shift</kbd>+<kbd>command</kbd>+<kbd>G</kbd>

- Output log of all macOS downloaded content

```shell
sqlite3 ~/Library/Preferences/com.apple.LaunchServices.QuarantineEventsV* 'select LSQuarantineDataURLString from LSQuarantineEvent'
```

- Remove log of all macOS downloaded content

```shell
sqlite3 ~/Library/Preferences/com.apple.LaunchServices.QuarantineEventsV* 'delete from LSQuarantineEvent'
```

- Install [Homebrew](https://brew.sh), the macOS package manager

```shell
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

- Elevate to root

```console
foo@bar:~$ sudo su
Password:🗝
```

- Copy contents of `id_rsa.pub` file to your clipboard

```shell
pbcopy < ~/.ssh/id_rsa.pub
```

- Display Time Machine Snapshots

```shell
tmutil listlocalsnapshots /
```

The terminal will display Snapshots like:
    `com.apple.TimeMachine.2018-03-01-00201`

- Delete Time Machine Snapshots

```shell
tmutil deletelocalsnapshots 2018-03-01-002010
```

## Android Development

- Reboot Android device to bootloader

```shell
adb reboot bootloader
```

- Reboot Android device to fastboot (*non-Samsung*)

```shell
adb reboot fastboot
```

- Wipe Android device's User data (_Cracked screen, need to wipe?_)

```shell
adb fastboot -w
```

- OEM Unlock Android device bootloader

```shell
fastboot oem unlock
```

- Flash the bootloader partition with the file dragged into the console window

```shell
fastboot flash bootloder 
```

- Erase Dalvik cache

```shell
fastboot erase cache
```

- Reboot Android device (from Fastboot)

```shell
fastboot reboot
```

### Android Studio

- Enable keyboard input without editing the `config.ini`:

Tools → Android → AVD Manager →✏️→ Show Advanced Settings (scroll to bottom) → Enable Keyboard Input

## Webserver Development

- Install packages necessary to host webpages

```shell
sudo apt update && sudo apt install php apache2 libapache2-mod-php php-curl libapache2-mod-auth-mysql mysql-server php-mysql phpmyadmin
```

- Setup MySQL

```shell
mysql_secure_installation
mysql -u root -p
```

- Enable Apache2 rewrite module

```shell
a2enmod rewrite
```

- Enable headers rewrite module

```shell
a2enmod headers
```

- Enable mcrypt

```shell
sudo php5enmod mcrypt
```

- Restart Apache

```shell
sudo service apache2 restart
```

- Install Remote Sublime Text Binary

```shell
sudo wget -O /usr/local/bin/rmate https://raw.github.com/aurora/rmate/master/rmate && sudo chmod a+x /usr/local/bin/rmate
```

- Edit `mysql` config

```shell
rmate /etc/mysql/my.cnf
```

- Enable `mysqli`

```shell
rmate /etc/php/7.0/apache2/php.ini
```

- Make `phpMyAdmin` viewable

```shell
sudo ln -s /usr/share/phpmyadmin /var/www/html/phpmyadmin

```

- **Edit Apache Configuration**

```shell
rmate /etc/apache2/apache2.conf
```

- **View Apache Error Log**

```shell
rmate /var/log/apache2/error.log
```

- Update `cURL`

```shell
! /usr/bin/env bash
```

- Install any build-dependencies necessary for `cURL`

```shell
sudo apt-get build-dep curl
```

- Get latest `libcurl` (as of: **Feb 25, 2016**)

```shell
mkdir ~/curl
cd ~/curl
wget http://curl.haxx.se/download/curl-7.50.2.tar.bz2
tar -xvjf curl-7.50.2.tar.bz2
cd curl-7.50.2
```
  
>_In Review_: Symbolic Link `ln -s` [current-target] [new-location]

- Update `SSL` (Avoid **Heart Bleed**)
    + First, ensure `make` is installed

```shell
sudo apt-get install make
```

- Download openSSL

```shell
wget https://www.openssl.org/source/openssl-1.1.0h.tar.gz
```

- Decompress and enter new directory

```shell
tar -xzvf openssl-1.1.0h.tar.gz
cd openssl-1.0.2g
```

- Configure openSSL

```shell
sudo ./config -Wl,--enable-new-dtags,-rpath,'$(LIBRPATH)'
```

- Compile openSSL

```shell
sudo make
```

- Install openSSL

```shell
sudo make install
```

- Restart

```shell
sudo reboot
```

- Verify openSSL version

```shell
openssl version -v
```

- Allow `Access-Control` to share Font cross-site
- Edit Apache2 Configuration:

```ApacheConf
<FilesMatch "\.(ttf|otf|eot|woff)$">
  <IfModule mod_headers.c>
    Header set Access-Control-Allow-Origin "*"
  </IfModule>
</FilesMatch>
```

- **SSL Certificates** with [_Let's Encrypt_](https://letsencrypt.org/)
    + First, add the repository:

    ```shell
    sudo add-apt-repository ppa:certbot/certbot
    ```
  
    + press <kbd>enter</kbd> to accept.  Next, update the package and install

    ```shell
    sudo apt update && sudo apt install python-certbot-apache
    ```
  
    + Ensure `apache2.conf` contains port 80 entry for domain(s) being added
    + Generate SSL Certificate
        * `certonly` assumes you will manually configure SSL Certificate config

    ```shell
    certbot --apache certonly -d domain.com -d www.domain.com -d sub1.domain.com -d sub2.domain.com -d sub3.domain.com
    ```
  
    + Add to existing SSL Certificate
        * Ensure the original 'domain.com' is first in the list:

    ```shell
    certbot --apache certonly --expand -d domain.com -d www.domain.com -d sub1.domain.com -d sub2.domain.com -d sub3.domain.com -d sub4.domain.com
    ```

- Remove a _Let's Encrypt_ SSL Certificate

```shell
rm -rf /etc/letsencrypt/archive/domain.com/
rm -rf /etc/letsencrypt/live/domain.com/
rm -rf /etc/letsencrypt/renewal/domain.com.conf
```

- Edit SSL Certificate configuration

```shell
rmate /etc/apache2/sites-available/000-default-le-ssl.conf
```

- Set up Auto-Renewal
To run the renewal check daily, we will use `cron`, a standard system service for running periodic jobs. We tell `cron` what to do by opening and editing a file called a `crontab`

```bash
sudo crontab -e
```

Your text editor will open the default crontab which is a text file with some help text in it. Paste in the following line at the end of the file, then save and close it:

```bash
. . .
15 3 * * * /usr/bin/certbot renew --quiet
```

The `15 3 * * *` part of this line means "run the following command at 3:15 am, every day". You may choose any time.

The `renew` command for Certbot will check all certificates installed on the system and update any that are set to expire in less than thirty days. `--quiet` tells Certbot not to output information nor wait for user input.

`cron` will now run this command daily. Because we installed our certificates using the `--apache` plugin, Apache will also be reloaded to ensure the new certificates are used.

## Linux Stuff

- Print Working Directory

```bash
pwd
```

+ Shortcuts
    * `id username`
        - List primary and secondary groups for `username`
    * `ls ~`
        - List contents of home directory

+ User Administration

- Add a `username` and assign secondary group: `tomcat7`

```bash
sudo useradd -G tomcat7 -m username
```

- Recursively delete user and /home directory

```bash
sudo userdel -r username
```

- Assign primary group named `primarygroup` for user named `username`

```bash
sudo usermod -g primarygroup username
```

- Modify the secondary group(s) (comma,delimited,list) of `username`

```bash
sudo usermod -G admin,adm,merchant,issuer,username username
```

- Add a new group named `groupname`

```bash
sudo groupadd groupname
```

- To remove a user from a group, use the gpasswd command with the -d (short for delete) option as follows

```bash
gpasswd -d userName groupExiting
```

- Recursively change the owner of file `directoryname` to `groupname`

```bash
sudo chgrp -R groupname directoryname
```

- Change shell to bash (**bash history**) for `username`

```bash
sudo chsh -s /bin/bash username
```

- BASH Aliases
    + Create/Edit `~/.bash_aliases`
    + Add:
        * `alias rsub='rmate $1'`
        * _no whitespace around '='_
        
- Modify file permissions with `chmod a+x`

```bash
chmod a+x ~/.bash_aliases
```

- To read and execute the contents of a file/script use the `Source` command
(the following example loads the bash aliases file)

```bash
source ~/.bash_aliases
```

- Find all files owned by `jacob`, change owner to `jason` and group owner to `groupname`

```bash
sudo find .-user jacob -exec chown jason:groupname {} \;
```

## Sublime Text

- Open `.ssh/config` in Sublime Text locally

```bash
subl ~/.ssh/config
```

- Enable remote Sublime Text editting, add

 ```shell
Host domain.com
RemoteForward 52698 127.0.0.1:52698
```

## GitHub Custom Emotes

Use these emotes anywhere on GitHub (only)

| emote | shortcode |
|:--|:--|
|:bowtie:|`:bowtie:`|
|:neckbeard:|`:neckbeard:`|
|:octocat:|`:octocat:`|
|:shipit:|`:shipit:`|
|:trollface:|`:trollface:`|
|:suspect:|`:suspect:`|
|:hurtrealbad:|`:hurtrealbad:`|
|:feelsgood:|`:feelsgood:`|
|:goberserk:|`:goberserk:`|
|:finnadie:|`:finnadie:`|
|:rage1:|`:rage1:`|
|:rage1:|`:rage1:`|
|:rage3:|`:rage3:`|
|:rage4:|`:rage4:`|
|:godmode:|`:godmode:`

## Contributors

![GitHub Contributors Image](https://contrib.rocks/image?repo=jaechow/info)

![Your Repository's Stats](https://github-readme-stats.vercel.app/api?username=jaechow&show_icons=true)

