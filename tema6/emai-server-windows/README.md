# Servidor de Correo - Windows 2016 Server

```
Nombre      : Alejandro de Paz Hernández
```

# 1. Introducción

Vamos a instalar y configurar dos servicios de correo en una máquina Windows 2016 Server. Primero, instalaremos el servicio SMTP que viene de forma nativa en Windows a través del administrador de aplicaciones (IIS) 6.0. Una vez hayamos configurado y probado este servicio de correo, instalaremos hMailServer; un servidor de correo de código abierto que nos ofrece más posibilidades y un mejor funcionamiento

---

# 2. Servicio SMTP

Instalamos el servicio SMTP, para ello `Administrador del servidor → Agregar roles y características`:

![](img/1.png)

![](img/3.png)

Una vez instalado, vamos a `Herramientas → Administrador de Internet Information Services (IIS) 6.0` para acceder a la configuración del servicio. Abrimos la pestaña de propiedades y configuramos lo siguiente:

* Establecemos como IP todas las no asignadas y limitamos el número de conexiones a 50:

![](img/5.png)

* Habilitamos el registro en formate W3C, diario y en una carpeta concreta:

![](img/8.png)

![](img/7.png)

* Habilitamos el acceso anónimo:

![](img/6.png)

* Aplicamos los cambios y reiniciamos el servicio.

* Accedemos a la sección de `Dominios` y comprobamos que existe el dominio predeterminado:

![](img/9.png)

* Creamos un nuevo dominio de tipo alias:

![](img/srd3.png)

![](img/srd4.png)

* Modificamos el DNS, añadiendo una nueva zona y los siguientes registros:

![](img/srd.png)

* Comprobamos la existencia de las carpetas de correo creadas en `C:\Inetpub\mailroot`:

![](img/12.png)

Vamos al cliente Windows y comprobamos el acceso a los registros que hemos creado en el DNS:

![](img/srd2.png)

Descargamos el cliente de correo Thunderbird y añadimos cuentas de correo asociadas a nuestro dominio:

![](img/26.png)

![](img/25.png)

Al intentar añadirlo nos aparecerán varias advertencias de seguridad, las ignoramos y continuamos:

![](img/27.png)

![](img/28.png)

Vemos que la cuenta se crea correctamente:

![](img/29.png)

Habilitamos la autenticación básica desde el servidor y añadimos dos nuevos usuarios; uno anónimo (usuarioprueba) y otro que pertenezca a Active Directory (diego):

![](img/31.png)

Probamos a enviar un correo de alejandro a diego:

![](img/32.png)

![](img/33.png)

Nos vamos al servidor y comprobamos las carpetas `C:\Inetpub\mailroot`. Dentro de `Drop` veremos el correo que hemos enviado:

![](img/34.png)

Repetimos lo mismo para el usuario anónimo:

![](img/35.png)

![](img/36.png)


# 3. hMailServer

Desinstalamos el servicio SMTP que hemos agregado previamente e instalamos hMailServer. Dejamos las opciones por defecto y finalizamos la instalación:

![](img/45.png)

Una vez finalizada, empezamos a configurar el servidor:

* Agregamos una contraseña para entrar al servidor:

![](img/46.png)

* Añadimos dos nuevos dominios (`Domains → Add`) que se llamarán **asir.edu** y **srd.edu**:

![](img/47.png)

* Si ejecutamos un diágnostico sobre los dominios que hemos creado, veremos que nos aparecen dos errores: uno de backup y otro de registro MX. El primero lo solucionamos asignando una carpeta donde guardar las copias de seguridad en `Utilities → Backup`:

![](img/49.png)

Para el segundo, creamos dos nuevas zonas de búsqueda directa (srd.edu y asir.edu) y añadimos los siguientes hosts:

![](img/58.png)

![](img/59.png)

Si ahora realizamos los diagnósticos vemos que no hay ningún error:

![](img/60.png)

![](img/61.png)

* Añadimos dos cuentas en cada dominio. Para la primera, **ricky@asir.edu**, habilitamos la firma y el mensaje de autorespuesta:

![](img/50.png)

![](img/51.png)

![](img/52.png)

Para la segunda, **john@asir.edu**, habilitamos el reenvío/redirección de correo hacia ricky@asir.edu:

![](img/53.png)

![](img/54.png)

Añadimos las cuentas restantes:

![](img/55.png)

![](img/56.png)

Dentro de hMailServer tenemos varias opciones de configuración:

* Podemos elegir los protocolos que vamos a permitir/utilizar en nuestro servidor:

![](img/62.png)

* Podemos crear un filtro anti-spam. También tenemos integrado el software de SpamAssassin, que nos permite marcar como spam los mensajes de cierto host concreto:

![](img/63.png)

![](img/64.png)

* Dentro de las opciones avanzadas, podemos auto banear a un cliente después de varios intentos de inicio de sesión fallidos. Existe también la posibilidad de bloquear rangos de IP's, establecer certificados SSL...:

![](img/65.png)

![](img/66.png)

Nos vamos al cliente Windows y configuramos las cuentas en Thunderbird. Tenemos que seleccionar la configuración **POP3**, ya que **IMAP** dará error:

![](img/68.png)

![](img/69.png)

![](img/70.png)

Repetimos lo mismo para todas las cuentas y probamos el envío y recepción de mensajes:

* De `john@asir.edu` a `jason@srd.edu`:

![](img/74.png)

* De `john@asir.edu` a `ray@srd.edu`:

![](img/75.png)

* Si enviamos un correo a `john@asir.edu`, en este caso desde `jason@srd.edu`, el correo se reenviará directamente a `ricky@asir.edu` y esta a su vez mandará un correo de autorespuesta:
    
    * Reenvío automático: 

    ![](img/77.png)

    * Respuesta automática:

    ![](img/78.png)

    ![](img/79.png)

* Por último, creamos una lista de distribución. Esto nos permitirá enviar un mismo correo a varias personas utilizando una sola dirección de correo:

![](img/80.png)

Añadimos como miembros a los dos usuarios de asir.edu (ricky y john). Para realizar las comprobaciones, marcamos la casilla `Keep original message` en las opciones de reenvío de john. De esta forma el mensaje se reenviará pero también aparecerá en su bandeja de entrada:

![](img/83.png)

Enviamos un correo a `empleados@asir.edu` y comprobamos:

![](img/84.png)

![](img/85.png)
    















