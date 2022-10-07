# Configuración e instalación de servicio DHCP en Windows

```
Nombre      : Alejandro de Paz Hernández
Curso       : 2º de Ciclo Superior de Administración de Sistemas Informáticos en Red
```

# 1. Introducción

En esta práctica vamos a configurar e instalar el servicio DHCP (Dynamic Host Configuration Protocol) en una máquina Windows Server 2016. Este servicio se utiliza en entornos cliente-servidor, de forma que proporcione la información establecida en el servidor al cliente (o clientes) automáticamente. Dicha información consiste en direcciones IP, máscaras de subred, puertas de enlace... En definitiva, información relacionada con la red.

---

# 2. Instalación del servicio DHCP

- Entramos en la máquina Windows Server y vamos a `Administrar el Servidor → Agregar roles y características`. Cuando lleguemos a roles del servidor, seleccionamos `Servidor DHCP` e instalamos:

![](img/1.png)

![](img/2.png)

- Una vez finalizada la instalación, nos aparecerá un triángulo amarillo en el administrador del servidor. Clickamos ahí e introducimos las credenciales de Administrador para dar de alta el servicio DHCP:

![](img/3.png)

## 2.1 Ámbitos
