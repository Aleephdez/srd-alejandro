# Servicio de Streaming - Ubuntu 18.04

```
Alejandro de Paz Hernández
```

# 1. Introducción

Vamos a instalar y configurar un servidor de streaming, esta vez en Linux utilizando **Icecas2t** y **ices2**.

---

# 2. Icecast2

Empezamos descargando e instalando el paquete **icecast2**:

![](img/1.png)

Una vez instalado, editamos el fichero de configuración `/etc/icecast2/icecast.xml` y modificamos las etiquetas `<source-password>, <admin-user> y <admin-password>` con los datos que queramos:

![](img/2.png)

Editamos también el fichero `/etc/default/icecast` y añadimos la siguiente línea:

![](img/3.png)

Iniciamos el servicio e instalamos el codificador **ices2**:

![](img/4.png)

Creamos un directorio para el codificador y copiamos el fichero de configuración por defecto:

![](img/5.png)

Editamos dicho fichero e introducimos la información de nuestra radio:

![](img/6.png)

Introducimos también la información referente al puerto de escucha y el punto de montaje. Si tenemos un servidor apache activo, tendremos que cambiar el puerto 8000, ya que Apache lo estará utilizando:

![](img/7.png)

Descargamos ficheros de audio en formato *.ogg* e introducimos las rutas en el fichero `/etc/icecast2/playlist.txt`:

![](img/8.png)

Creamos el directorio `/var/log/ices2` y lo introducimos en el fichero de configuración de **ices2**. Ejecutamos el codificador en segundo plano y accedemos desde un navegador:

![](img/22.png)

![](img/9.png)

Vemos que ya desde este panel tenemos la radio funcionando. Entramos al panel de administración con las credenciales definidas anteriormente:

![](img/12.png)

![](img/10.png)

![](img/11.png)

![](img/13.png)

Podemos hacer lo mismo desde un cliente Windows, por ejemplo:

![](img/19.png)

![](img/20.png)

![](img/21.png)

Por último, podemos reproducir el audio desde un reproductor multimedia como **VLC**. Para ello, nos vamos a `Medio > Emitir > Red`:

![](img/28.png)

![](img/29.png)

![](img/30.png)

![](img/31.png)







