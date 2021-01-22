# Practica12-IAW
En primer lugar vamos a la pagina oficial de Wordpress (https://bitnami.com/stack/wordpress/cloud/aws/amis) y en el apartado On the cloud vamos a single-tier, es decir una única capa y cogemos la primera AMI.

Al pinchar sobre el enlace nos lleva directamente a Amazon al panel de control.

Una vez dentro de Amazon elegimos 2GB de memoria y abrimos el puerto 80 y el 443, es decir el HTTP y el HTTPS.

Una vez hecho esto se inicia la instancia y debemos obtener el usuario y la contraseña para poder concectarnos y administrarla. Para localizar el usuario y la contraseña entramos en la pestaá acciones dentro de ahí en monitoreo y solución de problemas y por ultimo en obtener registros del sistema.

Lo que debemos hacer ahora es poder acceder a phpMyadmin y esto se hace mediante un túnel SSH. Sin hacer esto no podemos conectarnos al panel de control de phpMyadmin.
El túnel se crea de la siguiente forma : ssh -N -L 8080:127.0.0.1:80 -i clave_aws.pem bitnami@ip_maquina.

Con esto estamos haciendo que nuestro puerto 8080 y la direccion localhost se enlacen con la direccion ip de la máquina y con el puerto 80. Entonces al acceder a través de la URL 127.0.0.1:8080 entramos al panel de control de phpMyadmin.
