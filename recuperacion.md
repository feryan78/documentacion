# Recuperación Practicas

* Crear un nuevo volumen para la maquina virtual, clic derecho en localhost, en detalles

* Vamos a almacenamiento y creamos un nuevo volumen

![Darle clic en nuevo volumen](https://github.com/feryan78/documentacion/blob/master/imagenes/1.png?raw=true)

* Darle un nombre a nuestro nuevo volumen, darle formato qcow2 y el tamaño de 8GB
![Llenar los datos de nuestro nuevo volumen](https://github.com/feryan78/documentacion/blob/master/imagenes/2.png?raw=true)

* Deberia aparecer nuestro nuevo volumen en Almacenamiento
![Verificar que sea del tamaño y formato deseado](https://github.com/feryan78/documentacion/blob/master/imagenes/3.png?raw=true)

* Luego abrimos nuestra virtual y vamos al icono de detalles
![Detalles de nuestra virtual](https://github.com/feryan78/documentacion/blob/master/imagenes/4.png?raw=true)

* Agregar nuevo hardware y elegir storage, ahi elegir administrado y explorar
![Agregar hardware y explorar](https://github.com/feryan78/documentacion/blob/master/imagenes/5.png?raw=true)

* Escoger nuestro volumen nuevo
![Elegir el volumen](https://github.com/feryan78/documentacion/blob/master/imagenes/6.png?raw=true)

* Escoger tipo dispositivo "SCII" y en formato "RAW" o "qcow2" (dependiendo de la version de virtmanager)
![Escoger el tipo y fomato de nuestro nuevo dispositivo](https://github.com/feryan78/documentacion/blob/master/imagenes/7.png?raw=true)

* Ya deberia estar el hardware agregado en nuestros detalles
![Verificar que este agregado nuestro nuevo hardware](https://github.com/feryan78/documentacion/blob/master/imagenes/8.png?raw=true)

* Iniciar la virtual, hay q darle formato a nuestro nuevo disco, para ello, primero vemos donde esta nuestro disco nuevo
![Usamos fdisk -l para verificar nuestro nuevo disco](https://github.com/feryan78/documentacion/blob/master/imagenes/9.png?raw=true)

![Nuestro nuevo disco esta en /dev/sdc](https://github.com/feryan78/documentacion/blob/master/imagenes/10.png?raw=true)

* Debemos crear las particiones para nuestros grupos de volumenes
![cfdisk /dev/sdc](https://github.com/feryan78/documentacion/blob/master/imagenes/11.png?raw=true)

* Crear las particiones de tipo "primaria"
![Crear la primera particion](https://github.com/feryan78/documentacion/blob/master/imagenes/12.png?raw=true)
![Escoger write](https://github.com/feryan78/documentacion/blob/master/imagenes/13.png?raw=true)
![Crear nuestra 2da particion](https://github.com/feryan78/documentacion/blob/master/imagenes/14.png?raw=true)
![Escoger tambien de tipo primaria](https://github.com/feryan78/documentacion/blob/master/imagenes/15.png?raw=true)
![Escoger write](https://github.com/feryan78/documentacion/blob/master/imagenes/16.png?raw=true)

* Verificar con fdisk que se han creado las particiones
![Verificar con fdisk -l](https://github.com/feryan78/documentacion/blob/master/imagenes/17.png?raw=true)

* Creamos nuestros volumenes fisicos
![pvcreate /dev/sdc1 y /dev/sdc2](https://github.com/feryan78/documentacion/blob/master/imagenes/18.png?raw=true)

* Creamos nuestros grupos de volumenes
![vgcreate SISTEMAS-kvm01 y SISTEMAS-kvm02](https://github.com/feryan78/documentacion/blob/master/imagenes/19.png?raw=true)

* Creamos nuestros volumenes logicos
![lvcreate -L tamaño -n nombrevolumen nombregrupo](https://github.com/feryan78/documentacion/blob/master/imagenes/20.png?raw=true)

* Usamos lvs para verificar nuestros volumenes logicos

* Ahora debemos darle un sistema de archivos a los volumen que creamos
![mkfs.ext3 -m 0 /dev/mapper/SISTEMAS--kvm0x-volumen0X](https://github.com/feryan78/documentacion/blob/master/imagenes/21.png?raw=true)

* Verificamos nuestros grupos de volumenes
![vgdisplay](https://github.com/feryan78/documentacion/blob/master/imagenes/22.png?raw=true)
![vgdisplay](https://github.com/feryan78/documentacion/blob/master/imagenes/23.png?raw=true)

* Verificamos nuestros volumenes logicos
![pvdisplay](https://github.com/feryan78/documentacion/blob/master/imagenes/24.png?raw=true)

**MUCHAS GRACIAS**