# Practica 12 - Wordpress con Bitnami
En esta práctica se va a montar un sitio Wordpress utilizando una AMI de Bitnami.

## CLAVE
Este apartado lo considero bastante importante porque me pasó que cuando estaba terminando la práctica tuve que rehacerlo por esto que voy a contar a continuación.

En un momento de la práctica hay que hacer un tunel SSH y yo como trabajo con Windows lo hago a través de Putty, entonces uno de los pasos es poner el par de claves ssh de amazon que tiene cada máquina y las mías siempre son .pem pero Putty no reconoce ese formato, por lo que antes de nada hay que crear un par de claves nuevo en formato .ppk que esa clave si que es compatible con Putty.

![](https://raw.githubusercontent.com/joseean29/Practica12-IAW/main/images/001clave.PNG)

## CREACION MAQUINA VIRTUAL
En primer lugar vamos a la pagina oficial de Wordpress (https://bitnami.com/stack/wordpress/cloud/aws/amis) y en el apartado On the cloud vamos a single-tier, es decir una única capa y cogemos la primera AMI.

![](https://raw.githubusercontent.com/joseean29/Practica12-IAW/main/images/1.PNG)

Al pinchar sobre el enlace nos lleva directamente al Amazon al panel de control.

Para prevenir y evitar problemas con la instalación vamos a darle 2 GB de RAM a la instancia EC2.

![](https://raw.githubusercontent.com/joseean29/Practica12-IAW/main/images/2.PNG)

Debemos configurar los puertos de la siguiente manera para conectarnos por SSH y poder acceder por HTTP y HTTPS, abrimos los siguientes:

- SSH 22 (TCP)
- HTTP 80 (TCP)
- HTTPS 443 (TCP)

![](https://raw.githubusercontent.com/joseean29/Practica12-IAW/main/images/3.PNG)

Tras esto si entramos en la dirección IP de nuestra máquina vemos que entramos a Wordpress.

![](https://raw.githubusercontent.com/joseean29/Practica12-IAW/main/images/4.PNG)

Si pulsamos en el logo de bitnami de abajo a la derecha nos da información sobre como obtener la clave de administración del sitio, como acceder a PhpMyAdmin...

Ahora lo que nos interesa es conseguir la contraseña para entrar a Wordpress como administrador.

## LOCALIZAR CONTRASEÑA
El usuario se encuentra en la página en la que entramos al pinchar en el logo como hablé antes y es user, pero sin embargo para encontrar la contraseña debemos seleccionar la instancia y pinchar en `Acciones`, una vez ahí pinchamos a `Monitoreo y solución de problemas` y por último en `Obtener registros del sistema` y ahí subiendo un poco la podremos ver.

![](https://raw.githubusercontent.com/joseean29/Practica12-IAW/main/images/5.PNG)

Tras hacer esto ya ingresamos el usuario y la contraseña y accedemos a la administración de Wordpress sin problema.

![](https://raw.githubusercontent.com/joseean29/Practica12-IAW/main/images/6.PNG)

![](https://raw.githubusercontent.com/joseean29/Practica12-IAW/main/images/7.PNG)


## PHPMYADMIN - TUNEL SSH
Abrimos Putty y empezamos a configurarlo.

- Introducimos la dirección IP de la máquina en los campos `HostName` y en `Saved Sessions` y guardamos.

![](https://raw.githubusercontent.com/joseean29/Practica12-IAW/main/images/8.PNG)

- Vamos a la sección `Connection -> SSH -> Auth` e introducimos la ruta de la clave de la que hablé anteriormente.

![](https://raw.githubusercontent.com/joseean29/Practica12-IAW/main/images/9.PNG)

- Dentro de `Connection -> SSH -> Tunnels` escribimos 8080 en `Source Port`y localhost:80 en `Destination` y lo añadimos.

![](https://raw.githubusercontent.com/joseean29/Practica12-IAW/main/images/10.PNG)

- Ahora vamos a Connection -> Data y en `Auto-login username` añadimos bitnami, que es nuestro usuario.

![](https://raw.githubusercontent.com/joseean29/Practica12-IAW/main/images/11.PNG)

- Por último guardamos los cambios y le damos a open. 

![](https://raw.githubusercontent.com/joseean29/Practica12-IAW/main/images/12.PNG)

- Si queremos entrar a PhpMyAdmin debemos introducir la dirección http://127.0.0.1:8080/phpmyadmin 

![](https://raw.githubusercontent.com/joseean29/Practica12-IAW/main/images/13.PNG)

- Para entrar al panel de control entramos con el usuario `root` y la contraseña que conseguimos en el registro.

![](https://raw.githubusercontent.com/joseean29/Practica12-IAW/main/images/14.PNG)
