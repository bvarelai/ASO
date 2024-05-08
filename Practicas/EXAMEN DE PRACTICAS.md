# Anotaciones para el examen de practicas

## Grandes Diferencias
- La autenticacion PAM esta en sistemas Solaris, Linux y BSD (a excepcion de OpenBSD que usa una autenticacion BSD 
con una API distinta)
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
