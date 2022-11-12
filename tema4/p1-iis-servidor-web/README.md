# Windows Server 2016 IIS - Servidor Web básico

```
Nombre      : Alejandro de Paz Hernández

```

# 1. Introducción

En esta práctica vamos a configurar e instalar el servicio Web IIS en una máquina Windows 2016 Server para crear y alojar distintos sitios web.

---

# 2. Instalación del servidor web IIS

Para la instalación, nos vamos a `Agregar roles y características → Servidor Web (IIS)`. Agregaremos también la `Autenticación básica` y la `Autenticación de Windows`:

![](img/3.png)

# 3. Servidor web IIS 

Una vez instalado, comprobamos el acceso a la página web por defecto. Para ello, abrimos un navegador en el servidor e introducimos la dirección IP del servidor:

![](img/4.png)

Comprobamos que también podemos acceder desde un cliente, tanto por IP como por nombre:

> Hay que tener en cuenta que tendremos que poner nuestro servidor como servidor DNS del cliente para que resuelva el nombre

![](img/5.png)

![](img/6.png)

A continuación, vamos a modificar el `C:\Inetpub\wwwroot\index.html` para que la web por defecto nos muestre otra cosa:

![](img/8.png)

![](img/9.png)

Por último, creamos distintos directorios dentro de la ruta `C:\Inetpub\wwwroot\` y añadimos un `index.html` personalizado en cada uno. Al crear los directorios en la ruta física, nos aparecerán automáticamente en el Administrador de sitios web:

![](img/10.png)

Comprobamos el acceso a los distintos directorios, tanto por nombre como por dirección IP y tanto desde el cliente como desde el servidor:

![](img/11.png)

![](img/12.png)

![](img/13.png)

## 3.1 Sitios web independientes

Vamos a crear dos nuevos sitios web independientes. Para ello, vamos a `Herramientas → Administrador de Internet Information Services (IIS)` y creamos un nuevo sitio web llamado `alejandro.edu`:

![](img/17.png)

Para poder acceder a este sitio web, crearemos una nueva zona de búsqueda directa en el DNS con el mismo nombre. Si ahora nos vamos al navegador e introducimos la dirección, vemos lo siguiente:

![](img/18.png)

Y desde el cliente:

![](img/19.png)

A continuación, añadimos `recursos` como nuevo sitio web:

![](img/20.png)

Este nuevo sitio web será un subdominio de `alejandro.edu`, así que para ello tendremos que crear un subdominio dentro de la zona de búsqueda directa creada anteriormente. Nos vamos a un navegador y comprobamos:

![](img/21.png)

![](img/22.png)

El DNS nos quedaría de la siguiente forma:

![](img/24.png)

![](img/25.png)

Y los sitios web:

![](img/23.png)

## 3.2 Directorios virtuales

En este último apartado vamos añadir directorios virtuales al sitio web `alejandro.edu`. Esto nos permitirá acceder a directorios que se encuentren fuera de la dirección física establecida en la creación del sitio web, de forma que podamos acceder a archivos que estén en un disco duro o en cualquier otra parte. Para ello `Click derecho sobre el sitio web → Añadir directorio virtual`:

![](img/26.png)

Una vez creado, habilitamos el `Examen de directorios`. Esto hará que se listen automáticamente los ficheros y directorios cuando accedamos desde el navegador:

![](img/30.png)

Comprobamos accediendo desde el servidor y desde el cliente:

![](img/27.png)

![](img/28.png)

Añadimos un `index.html` a cada departamento y comprobamos:

![](img/31.png)

![](img/32.png)

![](img/33.png)

En nuestro caso, solo tenemos el `index.html`, pero si tuviéramos más archivos podríamos especificar cuál queremos mostrar de forma predeterminada:

![](img/34.png)

