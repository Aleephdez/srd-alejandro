# Listas de Distribución - Ubuntu 18.04

```
Alejandro de Paz Hernández
```

# 1. Introducción

Vamos a instalar y configurar un servidor de mensajería instantánea, que nos permitirá establecer comunicación en tiempo real entre dos o más usuarios en formato texto. Para ello, utilizaremos el software **OpenFire** y **Spark**.

---

# 2. phpList

> Para poder realizar la instalación de phpList, primero tendremos que tener instalado Apache, php y MySQL. 

Descargamos el .zip de la página oficial de **[phplist](https://www.phplist.org/download-phplist/)**. A continuación, creamos una base de datos y un usuario con todos los privilegios sobre esta:

![](img/1.png)

Una vez creada la base de datos y el usuario, los añadimos en el fichero de configuración de **phpList** `/var/www/phplist/public_html/lists/config/config.php`:

![](img/2.png)

Añadimos un nuevo virtualhost en Apache y lo habilitamos:

![](img/3.png)

![](img/4.png)

Si ahora nos dirigimos a `phplist.miempresa.com/lists/admin` desde un navegador, podremos empezar la instalación de **phpList** clickando en *Initialize database*:

![](img/5.png)

![](img/6.png)

Una vez finalizado, tendremos acceso al panel de administración de **phpList**:

![](img/7.png)

Desde ahí, podemos crear nuevos usuarios, campañas, listas...

* Para crear un usuario, nos vamos a `Suscriptores → Lista de todos los usuarios → Añadir un usuario`:

![](img/15.png)

* Para crear una lista, nos vamos a `Suscriptores → Lista de listas → Añadir una lista`:

![](img/11.png)

![](img/12.png)

![](img/13.png)

![](img/14.png)

* Para configurar una página de suscripción, nos vamos a `Config → Páginas de inscripción → Añadir una página de inscripción`:

![](img/17.png)

![](img/18.png)

![](img/19.png)

* Para configurar una campaña, nos vamos a `Campaña → Enviar nueva campaña`:

![](img/20.png)

![](img/21.png)

![](img/22.png)

![](img/23.png)

![](img/24.png)

![](img/25.png)




