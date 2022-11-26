# Servidor Web avanzado - PHP, MySQL, phpMyAdmin, FTP y Drupal

```
Nombre      : Alejandro de Paz Hernández
```

# 1. Introducción

En esta práctica vamos a instalar Drupal y Coppermine en nuestro servidor web, realizando la instalación desde un cliente. Para ello, primero instalaremos las herramientas necesarias para ello: PHP, MySQL, phpMyAdmin y FTP Server/Cliente.

---

# 2. Instalación de PHP

Empezamos descargando PHP. Vamos a descargar la última versión que salió en formato .msi, la 5.3.9:

![](img/2.png)

Es posible que no podamos instalarlo por no tener la característica **CGI** en el servidor web. En ese caso, vamos a `Administrador del servidor → Agregar roles y características → Servidor Web (IIS) → Servidor Web → Desarrollo de aplicaciones → CGI` e instalamos:

![](img/3.png)

Ahora sí, continuamos con la instalación de PHP:

![](img/4.png)

![](img/5.png)

Seleccionamos el fichero **index.php** como documento predeterminado de `miempresa.com` y lo creamos en la ruta física con el siguiente contenido `<?php phpinfo(); ?>`:

![](img/6.png)

![](img/7.png)

Si ahora accedemos a `miempresa.com`, veremos información sobre la versión de PHP que hemos instalado:

* Servidor:

![](img/8.png)

* Cliente:

![](img/9.png)

# 3. Instalación de MySQL y phpMyAdmin

Descargamos la versión de MySQL que sea compatible con la versión de PHP instalada. En este caso, será la 5.6.8.

En el asistente de instalación, seleccionamos **Server only**, para que no nos instale características de más:

![](img/12.png)

Continuamos con la instalación hasta llegar a la siguiente pantalla. Ahí asignamos una contraseña al usuario **root** y creamos un nuevo usuario **alejandro**:

![](img/15.png)

Finalizamos la instalación y pasamos a phpMyAdmin. De nuevo, tendremos que buscar una versión compatible con las versiones de MySQL y PHP que hemos instalado. En este caso, la versión será la 3.5.0. Descargamos el archivo .zip y lo extraemos en `C:\miEmpresa\phpMyAdmin\`:

![](img/16.png)

![](img/17.png)

A continuación, creamos un nuevo sitio web para acceder a phpMyAdmin llamado `phpmyadmin.miempresa.com`:

![](img/18.png)

> Recordar crear un nuevo registro en el DNS.

Probamos el acceso a phpMyAdmin:

* Desde el servidor:

![](img/19.png)

![](img/20.png)

* Desde el cliente:

![](img/21.png)

![](img/22.png)

# 4. Instalación y configuración de FTP

Como servidor FTP utilizaremos **FileZilla** tanto en el cliente como en el servidor. Empezamos descargando e instalando **FileZilla Server**:

![](img/23.png)

![](img/24.png)

Una vez instalado, lo abrimos y nos vamos a `Settings → Rights management → Users → Add`. Creamos un nuevo usuario llamado **ftpuser** y le asignamos la carpeta `C:\miEmpresa\principal`, que es donde instalaremos **Drupal**. De esta forma, podremos pasar ficheros desde el cliente a esa carpeta:

![](img/26.png)

Creamos un nuevo sitio web llamado `ftp.miempresa.com` y comprobamos que el servidor FTP está bien configurado desde el propio servidor:

![](img/27.png)

![](img/28.png)

![](img/29.png)

Por último, nos vamos a la máquina cliente e instalamos **FileZilla Client**:

>NOTA: Para este paso he cambiado el cliente, de Windows 7 a Windows 10, ya que me era imposible instalar FileZilla en el cliente Windows 7.

Una vez instalado, introducimos el nombre o IP del servidor FTP, el usuario y contraseña y el puerto por el que nos vamos a conectar (21 por defecto)

![](img/30.png)

Vemos que todo funciona correctamente y tenemos acceso a la carpeta `C:\miEmpresa\principal\`. Gracias a esto, podremos trabajar desde el cliente a partir de ahora.

# 5. Instalación y configuración de Drupal

Al igual que en las instalaciones anteriores, tendremos que buscar una versión de **Drupal** compatible con las versiones de PHP, MySQL y phpMyAdmin. En este caso, utilizaremos la versión 6.19. Descargamos el .zip y lo extraemos en la máquina cliente. Utilizando el cliente FTP, lo pasamos al servidor, a la carpeta `C:\miEmpresa\principal`:

![](img/31.png)

Ahora nos vamos a phpMyAdmin y creamos la base de datos `cms` y el usuario `cms`, que tendrá todos los privilegios sobre dicha base de datos. Utilizaremos ambos para la instalación de Drupal:

![](img/33.png)

![](img/34.png)

![](img/35.png)

![](img/36.png)

Una vez tenemos todos los requisitos, empezamos con la instalación de Drupal. Para ello, tendremos que cambiar la ruta física de `miempresa.com` y asignarle la carpeta `drupal-6.19`. Tras hacer esto, entramos a `miempresa.com` y veremos lo siguiente:

![](img/37.png)

Hacemos exactamente lo que nos dice el mensaje de error. Nos vamos a la carpeta `C:\miEmpresa\principal\drupal-6.19\sites\default\` y copiamos el fichero `default.settings.php` en la misma carpeta pero con el nombre `settings.php`. A continuación, cambiamos los permisos de `drupal-6.19` y le damos permiso de escritura al grupo `Todos`.

> En este caso le hemos dado permiso de escritura a todos los usuarios ya que es la única forma de que no salte el error.

Introducimos la base de datos y el usuario que hemos creado previamente y continuamos con la instalación:

![](img/39.png)

![](img/40.png)

Nos saltará el siguiente warning por problemas con el servidor de correo. Lo ignoramos y continuamos al sitio web:

![](img/42.png)

Ahora ya tenemos Drupal instalado y solo nos queda configurarlo. Podemos instalar módulos y temas adicionales, para ello nos vamos a `www.drupal.org → Build → Modules` o `www.drupal.org → Build → Themes` y buscamos el complemento que queramos instalar (debe ser una versión compatible con nuestra versión de Drupal):

![](img/43.png)

Una vez encontremos tanto el complemento como la versión, descargamos el .zip, lo extraemos y copiamos en `C:\miEmpresa\principal\drupal-6.19\Modules` (si es un módulo) o `C:\miEmpresa\principal\drupal-6.19\Themes` (si es un tema) a través del cliente FTP:

![](img/46.png)

Si ahora nos vamos a Drupal en `miempresa.com`, podremos encontrar y activar lo que hemos instalado:

![](img/44.png)

![](img/47.png)

Para configurar 

# 5. Instalación y configuración de Coppermine

Para instalar **Coppermine**, repetimos lo que hemos hecho con Drupal. Descargamos el .zip en el cliente, extraemos el contenido y lo pasamos por FTP a la carpeta `C:\miEmpresa\gallery`. Esta carpeta será la ruta de acceso física de nuestro nuevo sitio web `gallery.miempresa.com`:

![](img/56.png)

Creamos la base de datos y el usuario `gallery`, que utilizaremos para la instalación:

![](img/57.png)

Una vez terminados los preparativos, entramos en `gallery.miempresa.com` y realizamos la instalación:

![](img/58.png)

![](img/59.png)

Seleccionamos el usuario y la base de datos:

![](img/60.png)

![](img/61.png)

Creamos un usuario para administrar Coppermine y finalizamos la instalación:

![](img/62.png)

![](img/63.png)

![](img/64.png)
