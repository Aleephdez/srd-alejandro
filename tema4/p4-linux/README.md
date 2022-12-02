# Servidor Web Apache - Linux

```
Nombre      : Alejandro de Paz Hernández
```

# 1. Introducción

En esta práctica vamos a configurar un servidor web Apache con sitios seguros y carpetas privadas protegidas. También realizaremos la instalación de un CMS, para lo que necesitaremos MySQL, phpMyAdmin y PHP.

---

# 2. Instalación y configuración de Apache

Empezamos instalando el servidor web Apache en una máquina Ubuntu:

![](img/1.png)

Comprobamos el acceso a la carpeta raíz del sitio web por defecto. Comprobamos también el acceso al sitio web desde el navegador:

![](img/2.png)

![](img/3.png)

Modificamos el fichero `/etc/hosts` y añadimos lo siguiente:

![](img/4.png)

> Podríamos hacer lo mismo modificando el servidor DNS y añadiendo un registro para `www.miempresa.com`

Comprobamos el acceso desde un navegador:

![](img/5.png)

Podemos reiniciar o recargar Apache utilizando el siguiente comando:

![](img/6.png)

Comprobamos que existen los ficheros `/var/log/apache2/error.log` y `/var/log/apache2/access.log`:

![](img/7.png)

## 2.1 Configuración de Virtual Hosts

Vamos a crear y configurar dos virtual hosts asociados a `miempresa.com`. El primero será `empleados.miempresa.com`.

### 2.1.1 Sitio web 1 (empleados)

Lo primero será crear la carpeta donde almacenaremos la información que cargará el sitio web, o lo que es lo mismo, la ruta de acceso física. Creamos un `index.html` dentro para comprobar que funciona correctamente al entrar desde el navegador:

![](img/12.png)

A continuación, añadimos el sitio web a `/etc/hosts`:

![](img/14.png)

Creamos el fichero `/etc/apache2/sites-available/empleados.conf` con la siguiente configuración:

![](img/13.png)

Por último, creamos un enlace simbólico al fichero anterior en `/etc/apache2/sites-enabled/`, que nos permitirá habilitar el sitio web y acceder a él:

![](img/15.png)

> También podemos crear el enlace simbólico utilizando el comando `a2ensite` y seleccionando el sitio web que queremos habilitar.

Comprobamos el acceso desde el navegador:

![](img/16.png)


### 2.1.2 Sitio web 2 (pagos)

Para este segundo sitio web vamos a generar un certificado autofirmado para que el acceso sea por **HTTPS**. Para ello, utilizaremos la herramienta **openssl** que se instala por defecto al instalar Apache:

Generamos una clave de 2048 bits.

![](img/17.png)



# 3. Instalación de PHP

Instalamos PHP:

![](img/8.png)

Creamos un `index.php` en `/var/www/html` (ruta de acceso física de `www.empleados.com`) y eliminamos el `index.html` que viene por defecto. Incluiremos lo siguiente en dicho fichero: `-<?php phpinfo(); ?>-`. Esto nos mostrará información de la versión de PHP que hemos instalado al acceder al sitio web:

![](img/10.png)

Por último, instalamos el paquete `libapache2-mod-php` que servirá de intérprete de PHP para Apache:

![](img/11.png)

# 4. Instalación de MySQL

Instalamos MySQL Server y el soporte PHP para MySQL con los siguientes comandos:

```
sudo apt-get install mysql-server

sudo apt-get install php-mysql
```
Comprobamos el acceso a MySQL:

![](img/55.png)

# 4. Instalación de phpMyAdmin

Para instalar phpMyAdmin, descargamos la última versión desde la página web oficial y descomprimimos el archivo. Lo haremos en el directorio `/var/www/phpmyadmin`, que será la ruta de acceso física del sitio web `phpmyadmin.miempresa.com`:

![](img/56.png)

![](img/57.png)

A continuación, creamos el virtual host desde el que accederemos a phpmyadmin:

![](img/58.png)

> Hay que añadir también una línea nueva en `/etc/hosts` para `phpmyadmin.miempresa.com`

Comprobamos el acceso desde un navegador al sitio web:

![](img/59.png)

Para poder acceder a phpMyAdmin, primero tendremos que configurar una contraseña para el usuario **root**, que por defecto no tiene contraseña y phpMyAdmin restringe el acceso a usuarios sin contraseña:

![](img/60.png)

Ahora sí, accedemos a phpMyAdmin:

![](img/62.png)

![](img/63.png)

# 5. Instalación y configuración de WordPress

Para finalizar, vamos a instalar y configurar WordPress. Descargamos el .zip de la página oficial de WordPress y lo descomprimimos en `/var/www/wordpress`:

![](img/65.png)

![](img/66.png)

Creamos un nuevo virtual host, donde instalaremos WordPress:

![](img/64.png)

> Añadir también una nueva línea en `/etc/hosts` para `miempresa.com`

Nos vamos a phpMyAdmin y creamos una base de datos y un usuario (con todos los privielgios sobre la base de datos) para WordPress. Una vez hecho eso, entramos en `miempresa.com` desde un navegador y comenzamos la instalación:

![](img/68.png)

Introducimos la base de datos y el usuario que hemos creado:

![](img/69.png)

Es posible que nos aparezca un error como el siguiente:

![](img/71.png)

En ese caso, hacemos lo que nos dice; crear el fichero `/var/www/wordpress/wp-config.php` y copiamos y pegamos el contenido que nos muestran:

![](img/70.png)

Continuamos la instalación. Asignamos un nombre al sitio y creamos un usuario que se encargará de administrar el sitio:

![](img/72.png)

Finalizamos la instalación:

![](img/73.png)

Ahora vamos a configurar una página en WordPress. Para ello, vamos a la pestaña `Páginas` en el panel izquierdo de administración

![](img/74.png)

![](img/78.png)

Añadimos una nueva página y la editamos:

![](img/79.png)

La publicamos y comprobamos el resultado:

![](img/80.png)