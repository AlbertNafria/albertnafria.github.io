---
layout: post
title: "Nube casera con Nextcloud"
date: 2021-03-03 19:45:15 CET
categories: jekyll update
---



## Una nube casera con Raspberry Pi

Dado que en mi día a día utilizo dos máquinas distintas, un MacBook Pro y un
portátil HP viejito con [Ubuntu Mate][UbuntuMate], decidí hacer un servidor de
Nextcloud en una Raspberry Pi 3 para tener así los ficheros sincronizados.

[Nextcloud][Nextcloud] es un proyecto *open source* para alojar contenido en un
servidor que, al ser código abierto, puedes instalar en un servidor propio y no
tener que pagar por los servicios. La verdad es que pienso que es más cómodo
pagar Google Drive o Dropbox y olvidarse de problemas, pero me hacía ilusión
tener la nube en casa.

Para poder tener un servidor Nexcloud en casa, solamente hace falta tener una
[Raspberry Pi][RaspberryPi] con una tarjeta MicroSD y conexión a internet.

## Instalación del sistema operativo

Para poner en marcha la Raspberry Pi, primero hay que instalarle un sistema
operativo en la tarjeta MicroSD. Yo me decanté por RaspberryOS, desarrollado por
la misma fundación que comercializa la placa, y perfectamente optimizado para ella.

Añadir un fichero vacío con nombre `ssh` y un fichero `wpa_supplicant` con la
información del wifi.

Para conectarse desde otra máquina mediante *ssh*, podemos encontrar la IP
mediante el comando `ping raspberrypi.local`.

Una vez instalado el SO, y tras conectarse a la Raspberry Pi mediante *ssh*,
hay que actualizar con la orden `sudo apt update` e instalar los siguientes
programas y dependencias:

```bash
sudo apt install -y vim tmux git nmap 
sudo apt install -y apache2 mariadb-server libapache2-mod-php
sudo apt install -y php-gd php-json php-mysql php-curl php-mbstring
sudo apt install -y php-intl php-mcrypt php-imagick php-xml php-zip
```

## Instalación de Nextcloud

Con el comando `wget` descargué la [versión más reciente][Nextcloud reciente] de
Nextcloud en el directorio `/srv/` de la Raspberry Pi. Lo descomprimí en el
mismo directorio y después creé un enlace simbólico al servidor Apache para
poderlo ver desde un navegador.

```bash
$ cd /srv
$ sudo mkdir nextcloud
$ sudo wget https://download.nextcloud.com/server/releases/nextcloud-20.0.7.zip -O /srv/nextcloud.zip
$ unzip nextcloud.zip
$ sudo ln -s /srv/nextcloud /var/www/html/nextcloud
$ sudo chown -R www-data:www-data /srv/nextcloud
```

Seguidamente configuré la base de datos con las órdenes que siguen:

```mysql
$ sudo mysql
CREATE USER 'nextcloud' IDENTIFIED BY 'password';
CREATE DATABASE nextcloud;
GRANT ALL PRIVILEGES ON nextcloud.* TO 'nextcloud'@localhost IDENTIFIED BY 'password';

```

Ahora ya está Nextcloud funcionando, así que desde otro ordenador nos conectamos
a la url `raspberrypi.local/nextcloud` desde un navegador. Aparecerá la interfaz
de Nextcloud que nos pedirá un nombre de usuario y contraseña. Después pedirá
los siguientes campos referidos a la base de datos:
* Database User: nextcloud
* Database Password: 'Contraseña de la base de datos'
* Database Name: nextcloud
* Host: localhost

Ahora ya podemos empezar a utilizar Nextcloud dentro de la red local,
conectándonos a la IP de la Raspberry Pi.

## Monitorizar temperatura con RPi-Monitor

Para poder monitorizar la Raspberry Pi desde un navegador, hay una aplicación
muy interesante, `rpimonitor`. Para poderla instalarla hay que tener antes los
siguientes certificados:

```bash
sudo apt-get install apt-transport-https ca-certificates
sudo wget https://goo.gl/vewCLL -O /etc/apt/sources.list.d/rpimonitor.list
sudo apt-key adv --recv-keys --keyserver keyserver.ubuntu.com 2C0D3C0F
sudo apt update
sudo apt install rpimonitor
```

Una vez está todo instalado podemos acceder desde el navegador a una interfaz
muy sobria desde donde controlar la Raspberry desde la URL `raspberrypi.local:8888`.
La primera vez que se instala `rpimonitor` hay que solucionar unos errores con
los siguientes comandos:

``` bash
$ sudo /etc/init.d/rpimonitor update
# Para automatizar el update
$ sudo /etc/init.d/rpimonitor install_auto_package_status_update
```

También cabe mencionar que para obtener la temperatura del procesador de la
Raspberry Pi desde la línea de comandos, se puede ejecutar:
``` bash
$ /opt/vc/bin/vcgencmd measure_temp
```

[UbuntuMate]:https://ubuntu-mate.org
[Nextcloud]:https://nextcloud.org
[RaspberryPi]:https://raspberrypi.org
[Nextcloud reciente]:https://download.nextcloud.com/server/releases/nextcloud-21.0.0.zip
