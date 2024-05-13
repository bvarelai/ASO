# Anotaciones para el examen de practicas

## Grandes Diferencias
- La autenticacion PAM esta en sistemas Solaris, Linux y BSD (a excepcion de OpenBSD que usa una autenticacion BSD 
con una API distinta)
## Maquinas con linux
- Tienen snapd (servicio en segundo plano que administra y mantiene los snaps), snap (interfaz de línea de comandos utilizada para buscar, instalar)
 y snap store (repositorio donde se publican y obtienen snaps) 

## Maquina Devuan
- No tiene systemd, tiene sysvinit. Por lo que no se pueden hacer comandos como systemctl, journald, etc...
- EN este caso no venia con una particion swap (si miras df -h no sale, ya que se metio como un fichero), para
ver que tiene swap habia que ir al /etc/fstap
- Si tiene apt instalado
- Las particiones son /dev/sda, sdb, sdc...
## Maquina OpenBSD
- Con sysmerge se actualizan los archivos de configuracion
- Las particiones estan en /dev/sd0a, sd0e...
- en /etc/fstap aparece que la swap es una particion
## Maquina Solaris 
- pkg update : para actualizar. Tambien esta pkgadd, pkginfo, pkgrm (En solaris 11 esto no esta)
- el grub esta en /rpool/boot/grub
- En /dev/rdsk/ estan las particiones
## Maquina Fedora
- Utuliza yum (etc/yum) y dnf para instalar paquetes
