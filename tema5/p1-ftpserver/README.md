# FTP Server - Windows y Linux

```
Nombre      : Alejandro de Paz Hernández
```

# 1. Introducción

En esta práctica vamos a instalar y configurar varios servidores FTP en Windows Server 2016 y en Ubuntu, comprobando el acceso y las distintas funciones desde un cliente.

---

# 2. Servidor FTP en Windows Server

Empezamos instalando el servidor FTP que nos ofrece el servidor web IIS desde el `Asistente de roles y características` de Windows Server:

![](img/1.png)

## 2.1 Servidor FTP 1

Una vez instalado, vamos a `Herramientas → Administrador de Internet Information Services (IIS) → Agregar sitio FTP`. Seleccionamos el nombre del sitio y le añadimos la ruta de acceso física:

![](img/2.png)

Seleccionamos la IP y el puerto. Lo crearemos sin SSL:

![](img/3.png)

> En caso de error al acceder al servidor FTP a través del navegador, es posible que tengamos que deshabilitar el nombre de host virtual.

Desmarcamos la autenticación anónima y añadimos al usuario **Administrador** como único usuario con acceso al servidor, con permisos de escritura y lectura:

![](img/4.png)

Si nos vamos al sitio FTP que hemos creado, veremos las siguientes opciones:

![](img/8.png)

- **Aislamiento de usuario FTP**: nos permite "encerrar" a cada usuario en la carpeta que queramos.
    
    ![](img/7.png)

- **Autenticación FTP**: nos permite habilitar/deshabilitar la autenticación básica y la anónima.

    ![](img/9.png)

- **Compatibilidad con el firewall**: nos permite configurar el servidor FTP para aceptar conexiones pasivas de un firewall externo.

    ![](img/10.png)

- **Configuración SSL de FTP**: nos permite cambiar la configuración de SSL del servidor.

    ![](img/11.png)

- **Examen de directorios FTP**: nos permite cambiar el estilo en el que se listan los directorios/archivos.

    ![](img/12.png)

- **Filtrado de solicitudes FTP**: nos permite configurar reglas de filtrado para el servicio FTP.

    ![](img/13.png)

- **Mensajes de FTP**: nos permite configurar un mensaje predeterminado que aparecerá al conectar con el servidor FTP.

    ![](img/14.png)

- **Registro FTP**: nos permite configurar la ruta en la que se guardan los ficheros **.log**.

    ![](img/15.png)

- **Reglas de autorización FTP**: nos permite añadir usuarios y cambiar los permisos de estos sobre el servidor FTP.

    ![](img/16.png)

- **Restricciones de direcciones IP y dominios de FTP**: nos permite restringir determinadas IPs y dominios para que no puedan acceder al servidor FTP.

    ![](img/17.png)

- **Sesiones actuales FTP**: nos muestra las sesiones abiertas con nuestro servidor FTP.

    ![](img/18.png)

Accedemos a través del navegador del servidor:

![](img/5.png)

![](img/6.png)

A través del explorador de archivos del servidor:

![](img/21.png)

![](img/22.png)

Probamos a subir un archivo desde el escritorio a `C:`:

![](img/23.png)

Hacemos lo mismo desde el cliente. Primero desde el navegador:

![](img/19.png)

![](img/20.png)

Y desde el explorador de archivos:

![](img/24.png)

Comprobamos que tenemos acceso a algunas de las carpetas:

![](img/24.png)

![](img/25.png)

Y probamos a descargar el archivo `prueba.txt`:

![](img/29.png)

A continuación, vamos a instalar `WinSCP`, un cliente STFP, en nuestra máquina cliente Windows 7. Realizamos la instalación dejando todas las opciones por defecto:

![](img/30.png)

Iniciamos el programa y probamos la conexión a nuestro servidor FTP:

![](img/31.png)

![](img/32.png)

Probamos la subida de archivos, pasando el archivo `srd-prueba.txt` a `C:/Users/Administrador/Documents/`:

![](img/33.png)

![](img/34.png)

## 2.2 Servidor FTP 2

Vamos a crear un segundo servidor FTP que tenga como ruta de acceso física `C:\inetpub\wwwroot`:

![](img/35.png)

Para poder tener activos los dos servidores FTP a la vez y no tener problemas, le asignaremos un puerto distinto a este segundo servidor. En este caso, utilizaremos el puerto `8080`. También podríamos solucionar esto utilizando los nombres de host virtuales, sin embargo, al habilitar esta opción, el servidor IIS da problemas y no permite el acceso por IP siquiera. Para este segundo servidor permitiremos el uso de certifiado SSL:

![](img/36.png)

Deshabilitamos la autentiación anónima y le damos acceso a todos los usuarios de **Active Directory** o, lo que es lo mismo, a todos los usuarios del servidor con permisos de lectura y escritura:

![](img/37.png)

Comprobamos el acceso desde el navegador del servidor con el usuario **diego**:

![](img/39.png)

![](img/38.png)

Y con el usuario **alejandro**:

![](img/41.png)

![](img/45.png)

Si intentamos entrar con un usuario que no pertenece al dominio, no nos dejará:

![](img/44.png)

Probamos el acceso desde el explorador de archivos del servidor con el usuario **carla**:

![](img/46.png)

![](img/47.png)

Por último, probamos el acceso desde el cliente a través de `WinSCP`:

![](img/50.png)

![](img/49.png)

Y pasamos el archivo `srd-prueba.txt`:

![](img/51.png)

Comprobamos que también podemos descargar archivos, descargando `index.html`:

![](img/52.png)

> En caso de error al subir o descargar archivos tendremos que revisar los permisos sobre la carpeta `wwwroot` y asegurarnos de que los usuarios con los que estamos accediendo tienen permiso de **escritura** y **lectura** sobre dicha carpeta.

## 2.3 Servidor FTP 3

Vamos a crear un tercer y último servidor FTP. En este caso, le daremos como ruta de acceso física la carpeta de descargas del usuario **Administrador**:

![](img/59.png)

Al igual que antes, cambiaremos el puerto para que no haya interferencias con los otros dos servidores FTP. Esta vez utilizaremos el puerto 8000:

![](img/60.png)

En este caso, vamos a permitir la autenticación anónima. Tendrán acceso todos los usuarios del servidor con permiso de solo lectura:

![](img/61.png)

> En caso de error al acceder, tendremos que asegurarnos que el grupo **Todos** tiene permiso de lectura sobre la carpeta `C:\Users\Administradpr\Downloads`

Probamos el acceso desde el navegador y desde el explorador de archivos del servidor:

![](img/63.png)

![](img/64.png)

En ambos casos se logueará con el usuario **Anónimo** de forma predeterminada.

Nos vamos al cliente y comprobamos el acceso a través de `WinSCP`:

![](img/65.png)

![](img/66.png)

Si intentamos subir un archivo, nos mostrará un error:

![](img/67.png)

Sin embargo, sí que podemos descargar, por ejemplo, el archivo `phpMyAdmin.zip`:

![](img/68.png)

# 3. Servidor FTP en Ubuntu

# 3.1 SSH

Lo primero es asegurarnos de tener instalado el servicio `SSH` tanto en el servidor como en el cliente. Por lo general, estará instalado por defecto. En caso contrario, lo instalamos con `apt-get install ssh`.

A continuación, creamos dos usuarios con distintos privilegios. El primero, **ftp_admin**, pertenecerá al grupo **sudoers** y tendrá privilegios de **root**. El segundo, **ftp_user**, será un usuario más del sistema, sin privilegios especiales:

![](img/74.png)

Añadimos a **ftp_admin** al grupo sudoers:

![](img/70.png)

Cambiamos también el intérprete de terminal de ambos usuarios, de `sh` a `bash` en el fichero `/etc/passwd`:

![](img/75.png)

Comprobamos el acceso por SSH desde un cliente con ambos usuarios:

![](img/72.png)

![](img/73.png)

Probamos la ejecución de una aplicación gráfica a través de SSH desde el cliente. Para ello, añadimos la opción `-X` al comando `ssh`:

![](img/76.png)

> En caso de error, hay que comprobar que la opción `X11Forwarding yes` esté en el fichero de configuración `/etc/ssh/sshd_config`. También tenemos que asegurarnos de que el programa `xauth` esté instalado en el servidor. Otro posible error es que hayamos creado los usuarios sin directorio `/home`.

# 3.2 Servidor FTP

Vamos a comprobar el acceso al servidor FTP mediante SFTP desde el cliente. Lo haremos con el usuario **ftp_admin** primero:

![](img/77.png)

![](img/78.png)

Probamos la descarga de archivos, descargando tres ficheros de prueba de `/home/ftp_admin/Documentos` :

![](img/79.png)

![](img/80.png)

Y la subida de archivos, subiendo un pdf a `/home/alejandro/Documentos`:

![](img/81.png)

![](img/82.png)

A continuación, accedemos con el usuario **ftp_user**:

![](img/84.png)

Si intentamos listar/leer el directorio `/home/alejandro/` vemos que no tenemos permiso para ello. El único directorio sobre el que puede trabajar el usuario **ftp_user** es sobre su propio directorio `/home`. Podemos descargar archivos:

![](img/87.png)

![](img/86.png)

Y subirlos:

![](img/88.png)

# 3.3 SCP

También podemos hacer uso del comando `scp` para la subida de archivos. Vamos a subir el archivo `prueba.zip` a `/home/alejandro/Documentos` con el usuario **ftp_admin**:

![](img/89.png)

![](img/90.png)

Si intentamos hacer lo mismo con el usuario **ftp_user**, nos dará error por falta de permisos. Al igual que antes, solo podremos subir archivos al directorio `/home/ftp_user`:

![](img/91.png)

![](img/92.png)

# 3.3 PROFTPD

Para finalizar, vamos a instalar el paquete `proftpd` → `apt-get install proftpd`, un servidor FTP de código abierto. Una vez instalado, descomentamos la línea `DefaultRoot` del fichero de configuración `/etc/proftpd.conf`. Esto hará los usuarios ese encuentren en su directorio `/home` al entrar al servidor FTP.

Comprobamos el acceso desde la máquina servidor:

![](img/95.png)

Y desde el cliente:

![](img/94.png)

Probamos la descarga de un archivo con el usuario **ftp_admin** sobre `/home/alejandro/Documentos`:

![](img/96.png)

![](img/97.png)

Y probamos también la subida de archivos, subiendo el fichero `prueba.zip` a `/home/alejandro/Documentos`:

![](img/98.png)

![](img/99.png)

Vamos a entrar ahora con el usuario **ftp_user**:

![](img/100.png)

Si intentamos entrar al directorio `/home/alejandro` dará error:

![](img/101.png)

Al igual que antes, sólo podemos realizar operaciones sobre el directorio `/home` de **ftp_user**:

![](img/102.png)

![](img/103.png)


