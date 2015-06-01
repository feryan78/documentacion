# GNU/Linux
## Comandos basicos
* Listar archvios
```
ls -l (listado de archivos con el dueño)
```

* Resultado del comando
```
total 32
drwxr-xr-x 2 feryan feryan 4096 may 13 02:02 Descargas
drwxr-xr-x 2 feryan feryan 4096 may 13 07:53 Documentos
drwxr-xr-x 2 feryan feryan 4096 may 13 02:02 Escritorio
drwxr-xr-x 2 feryan feryan 4096 may 13 02:02 Imágenes
drwxr-xr-x 2 feryan feryan 4096 may 13 02:02 Música
drwxr-xr-x 2 feryan feryan 4096 may 13 02:02 Plantillas
drwxr-xr-x 2 feryan feryan 4096 may 13 02:02 Público
drwxr-xr-x 2 feryan feryan 4096 may 13 02:02 Vídeos
```

* Listar archivos, ordenar por fecha de modificacion
```
ls -lahtr
```

* Crear directorios
```
mkdir nombre_carpeta
```
```
mkdir -p /nombre_carpeta/subcarpeta
```

* Crea varios subdirectorios de una sola instruccion
```
mkdir /tmp/{c1,c2,c3,c4,c5,c6}
```
```
mkdir -p /dir/qqq/aaa/bbbb/{c1,c2,c3,c4,c5,c6}
```
```
. (punto) Directorio actual
~ Home del usuario
```
```
mkdir ./hola/
```
```
mkdir ~/hola/
```

* Crear un archivo vacio
```
touch nombre_archivo (tipo texto plano)
```

* Programas para editar archivos
```
nano, vi, vim, etc
```

* Crear archivo a partir del resultado de un comando se usa el simbolo **">", ">>"** para concatenar elresultado.

* Para buscar dentro de un archivo 
```
grep texto nombre_archivo
```

* Para que te despliegue el numero de la linea
```
grep -n texto nombre archivo
```

* Para buscar en todo un directorio
```
grep -nR aa . > resultado.txt
```

* Buscar archivo dentro de un directorio
```
find directorio -name nombre_archivo^Carpeta
```

* Buscar archivo sin conocer extension
```
find directorio -name nombre_arhchivo\*
```
**el \* es como comodin**

* Para conocer el manual de un comando
```
man nombre_comando
```

* Conocer donde esta los arhivos de un determinado comando
```
whereis nombre_comando
```

* Borrar archivos
```
rm nombre_archivo
```

* Borrar archivo de forma recursiva
```
rm -r nombre_archivo
```

* Ejecutar con privilegios de administrador
```
sudo mkdir /opt/bbb
```

* Para ingresar o salir a una carpeta o directorio
```
cd nombre_carpeta
```

* Se puede ingresar o salir de un subdirectorio directamente
```
cd /a/b/c/d/f/g/h/i/j/k
```
```
cd /a/b/c/d/f/g/h/i/j/k /../../../
```
```
cd ~
```

* Para instalar paquetes
```
apt-get install nombre_paquete
```
```
aptitude install nombre_paquete
```

* Archivo para configurar repositorio
```
/etc/apt/source.list
```

* Instalar paquete sudo
```
apt-get install sudo
```

* Comando para verificar nuestro grupo
```
groups
```

* Agregar usuario a un grupo (como root)
```
adduser nombre_usuario nombre_grupo
```

* Para ver nuestras tarjetas de red
```
lspci | grep -i network
```
```
lspci | grep -i ethernet
```

* Para ver si el driver esta en el repositorio
```
aptitude search nombre_driver
```

## Versionamiento y Manejo de Proyectos en Github

* Instalación de GIT
```
apt-get install git
```

* Crear carpeta de proyecto
```
mkdir proyecto
```

* Dentro del directorio ejecutar
```
git init
```

* Para adicionar tu repositorio en la web
```
git remote add origin
```

* Para añadir tu archivo
```
git add README.md
```

* Configurar usuario y correo
```
git config --global user.name "nombre_usuario"
git config --global user.email "correo_usuario@dominio"
```

* Hacer commit de nuestros cambios en nuestro repositorio
```
git commit -m "mensaje"
```

* Para subir nuestro cambio a la web
```
git push origin master
git remote -v (muestra nuestro repositorio y master)
```

* Pasos para GIT
```
git clone (solo una vez)
git add archivo/carpeta
git commit -m "mensaje"
git push origin master
```

## Virtualizacion

* **Para verificar si nuestro procesador soporta virtualizacion**

* Para procesadores INTEL
```
grep vmx /proc/cpuindo
```

* Para procesadores AMD
```
grep svm /proc/cpuindo
```

### Virtualizacion completa - KVM

* Instalacion de Paquetes
```
apt-get install qemu-kvm libvirt-bin virtinst vir-viewer
```

* Para administrar las maquinas virtuales en modo grafico GUI
```
apt-get install virt-manager
```

* Agregar usuarios al grupo kvm
```
adduser usuario kvm
adduser usuario libvirt
```

### Particionamiento con LVM

*  Estructura LVM
```
/boot
 LVM
	swap
    /root
    /home
    /usr
    /tmp
    /var
```

* Ver particiones en consola
```
df -h
```

* Ver información del grupo de volúmenes LVM
```
vgdisplay
```

* Desplegar información de los volúmenes lógicos de LVM
```
lvdisplay
```

* Ver tamaño libre de la particion LVM
```
vgs
```

* Información de los volumenes logicos
```
lvs
```

### Redimensionamiento de particiones

#### Pasos para aumentar espacio en tu volumen logico

* Correr el comando
```
lvextendend -L+"tamaño" "ruta del volumen logico"
```
Ver la ruta de nuestro disco usar **df -h**
Con **lvs** verificamos el nuevo tamaño de nuestra partición
Con **df -h** sigue mostrando el mismo tamaño, hay que redimensionar la partición

* Desmontar la particion
```
umount /dev/mapper/NOMBRE_PARTICION
```

* Verificar que este desmontada
```
df -h
```

* Verificar integridad de lo datos
```
e2fsck -f "ruta de la particion"
```

* Redimensionar el sistema de archivos
```
resize2fs "ruta de la particion"
```

* Montar la particion
```
mount "ruta particion"
```

* Verificar el tamaño nuevo
```
df -h
```

#### Pasos para reducir nuestra partición

* Desmontar la unidad
```
umount "particion"
```

* Verificar la integridad de la partición
```
e2fsck -f "ruta particion"
```

* Redimensionar el sistema de archivos reduciendolo
```
resize2fs "ruta particion" 500M
```

* Montar de nuevo la partición
```
mount "ruta particion"
```

* Reducir nuestro volumen logico
```
lvreduce -L 500M "ruta particion"
```

### Crear un nuevo volumen para la maquina virtual

* Clic derecho en localhost, y luego en detalles

* Vamos a almacenamiento y creamos un nuevo volumen

* Abrimos nuestra virtual y vamos al icono de detalles

* Agregar nuevo hardware y elegir storage, ahi elegir administrado y explorar ahi escoger tipo dispositivo "virtio disk", en formato "raw", esto no funciona con versiones antiguas de virtmanager, asi que hay q cambiar el dispositivo a SCSI y en formato "qcow2", de esa forma reconocera nuestro disco en la virtual

* Iniciar la virtual, hay q darle formato a nuestro nuevo disco, para ello, primero vemos donde esta nuestro disco nuevo:
```
fdisk -l
```

* Crear la partición nueva
```
cfdisk "ruta de nuestro nuevo disco"
```

* Vamos a la opcion "new", tipo de partcion "primaria" y asignamos 1gb, luego "write"

* Verificar de nuevo los discos duros
```
fdisk -l
```

* Para ver solo nuestra particion:
```
fdisk -l ruta_particion
```

* Ver el volumen fisico de nuestro volumen logico
```
pvdisplay
```

* Crear nuestro nuevo volumen fisico
```
pvcreate ruta_particion
```

* Crear volumen de grupo
```
vgcreate grupoA /dev/sda1
```

* Para crear un volumen logico
```
lvcreate -L tamaño -n nombrevolumen nombregrupo
```

* Para verificar nuestros volumenes logicos
```
lvs
```

* Darle un sistema de archivos al volumen que hemos creado
```
mkfs.ext3 -m 0 /dev/mapper/nombregrupo-volumen
```

* Crear el punto donde quieres montarlo
```
mkdir /mnt/punto_montaje
```

* Ahora montar el disco
```
mount /dev/mapper/nombregrupo-volumen /mnt/punto_montaje
```

* Si reiniciamos ya no aparecere nuestra partición, para que sea automatico editar el archivo
```
nano /etc/fstab
```

* Editar para añadira nuestra particion logica (ctrl+k para cortar y ctrĺ+u para pegar) verificar que este en ext3

### Ampliar tamaño de nuestro disco virtual

* Aumentar tamaño LVM de nuestro disco duro virtual (en nuestro host)
```
qemu-img resize "nombre disco.img" (qcow2) +15G
```

* En la maquina virtual entrar con root, verificar nuestro nuevo tamaño
```
fdisk -l
```

* Para poder particionar
```
cfdisk "directorio disco"
```
```
fdisk -l "directorio disco"
```

* Para cambiar el tamaño del LVM, primero redimensionar particion extendida, para eso usar gparted live cd para gestionar la partición, entrar modo live cd, "don't touch keymap", escoger idioma y poner 0

* Redimensionar el disco duro virtual
```
qemu-img resize ruta_disco +5G
```

* Bootear desde el CD-ROM (gparted.iso)
*expandir la partición extendida, desde el modo grafico*
*expandir la partición LVM, desde el modo grafico*
*reiniciar la maquina virtual*
*fdisk -l /ruta_particion*

## Manejo de Red

* Listar tarjetas de red del sistema
```
ls /sys/class/net/
```

* Para ver configuración tarjetas de red
```
/etc/network/interfaces
```

* Reiniciar el servicio de red
```
service networking restart
/etc/init.d/networking restart
```

* Para ver nuestras interfaces tambien podemos usar
```
ls /sys/class/net
```

* Mostrar nuestra IP
```
ip addr show
```

* Para ver de solo una interfaz
```
ip addr show eth0
```

* Para ver nuestras interfaces usamos
```
ifconfig
```

* Ver solo una interfaz
```
ifconfig eth0
```

* Configuración manual de interfaces
```
nano /etc/network/interfaces
```

* En el archivo cambiar de dhcp a static y añadir
```
address 192.168.122.100
netmask 255.255.255.0
gateway 192.168.122.1
```

* En el virtmanager hacer clic derecho en localhost, ahi entrar a redes virtuales y añadir una nueva. Colocar en la red 192.168.3.0, deshabilitar DHCP y cambiar la red fisica a "reenvio", en destino poner "cualquier dispositivo fisico" y en Modo usar NAT

* Para usar la nueva red virtual, en la maquina virtual entrar a detalles y cambiar la red para que use nuestra nueva red virtual

* Reiniciar el equipo

* Cambiar el archivo interfaces para que use nuestra nueva red

* Reiniciar el servicio y/o reiniciar el equipo

* Modificar el archivo /etc/resolv.conf modificar en DNS en nuestro caso el mismo gateway

* Para agregar otro DNS solo agregar otra linea
```
nameserver XXX.XXX.XXX.XXX
```

## Acceso Remoto mediante SSH

* Instalar el ssh (si no esta instalado)
```
apt-get install ssh
```

* Verificar puertos abiertos
```
netstat -natp
```

* Verificar un puerto especifico
```
netstat -natp | grep 22
```

* Cambiar el archivo de configuracion
```
nano /etc/ssh/sshd_config
```

* Cambiar la linea donde esta PubKeyAuthentication a no

* Reiniciar el servicio
```
/etc/init.d/ssh restart
service ssh restart
```

* Para ingresar remotamente
```
ssh nombreusuario@ip_equipo
```

* Para copiar un archivo en otro equipo
```
scp nombrearchivo usuario@ip_equipo:/directorio
```

* Copiar carpetas a otro equipo
```
scp -r /tmp/carpeta/ usuario@ip_equipo:/carpeta
```

* Por seguridad deshabilitar inicio de sesion con usuario "root"

* Editar el archivo sshd_config y poner "no" en la linea donde esta "PermitRootLogin"

* Ver quienes estan conectados con el comando
```
who
```

### Usar llave generada

* Crear una carpeta .ssh en nuestro home, si es que no esta creada

* Generar la llave publica
```
ssh-keygen -t rsa -b 2048
```

```
Generating public/private rsa key pair.
Enter file in which to save the key (/home/feryan/.ssh/id_rsa): 
Enter passphrase (empty for no passphrase): 
Enter same passphrase again: 
Your identification has been saved in /home/feryan/.ssh/id_rsa.
Your public key has been saved in /home/feryan/.ssh/id_rsa.pub.
The key fingerprint is:
60:0a:b6:ad:33:09:6b:fb:ca:43:aa:13:d2:e2:59:71 feryan@milicita
The key's randomart image is:
+--[ RSA 2048]----+
|                 |
|                 |
|  o   o          |
| . = E .         |
|... =   S        |
|++.+             |
|*+B              |
|=+.o             |
|o=+.             |
+-----------------+

```

* Para ver las llaves que se crearon
```
ls -l .ssh
```

* El id_rsa es la llave privada que solo debemos tener nosotros

* El id_rsa.pub es la llave publica que podemos compartir

* Para copiar nuestra llave a la maquina virtual
```
ssh-copy-id -i /home/usuario/.ssh/id_rsa.pub usuario@ip_equipo
```

* Debemos luego modificar el archivo ssh_config, modificar el PubKeyAuthentication a "yes"

* Reiniciar ssh


## Permisos, usuarios, directorios por Consola

* Para ver permisos de los archivos
```
ls -l
```
```
drwxr-xr-x nombrearchivo
```
Los 3 primeros son del usuario
Los 3 segundos son permisos de grupo
Y los 3 ultimos permisos para otros
```
r lectura 4
w escritura 2
x ejecucion 1
```

* Para cambiar permisos
```
chmod
```

* Para cambiar solo para otros
```
chmod o+w carpeta_archivo
chmod o-rwx carpeta_archivo
```

* Para todos los permisos
```
chmod -rwx carpeta_archivo
```

* Para dar permisos a los diferentes grupos solo sumar y poner el valor
```
chmod 437 carpeta_archivo
```
El usuario podra solo leer
El grupo escribir ejecutar
Y otros tendrán permisos totales

* Cambiar el dueño de un archivo o directorio
```
chown usuario hola.txt
```

* Para crear usuarios
```
sudo useradd usuario1
```

* Para cambiar contraseña del usuario
```
sudo passwd usuario1
```

* Para ver todos los usuarios de la maquina
```
getent passwd
```

* Para entrar con un usuario
```
sudo su - nombre_usuario
```

* Para crear usuario con datos más completo
```
sudo adduser nombreusuario
```
Llenar los datos y poner "yes"

**Gracias por todo**