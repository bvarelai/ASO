# Memoria de las Practicas ASO 2023-24
- VMSvGA : Para todos los casos
- VboxVGA : Para uno en particular
## Instalacion y configuración de la primera maquina
- **IMPORTANTE** : El controlador debe ser debe ser de tipo SATA   
ya que sino la instalacion de **OpenBSD** falla.
- Tambien **INSTALAR PRIMERO DEVUAN** y desde ahi crear las demas particiones para instalar openBSD, Solaris y syslinux
### Devuan Linux
### OpenBSD 
#### Para la clase desegunda
- **tar cvf fichero /usr/bin** : con esto creo un fichero para probar la clase
### Solaris
#### Tema de DNS en Solaris
- https://www.dc.fi.udc.es/~afyanez/Docencia/2022/Grado/ASO-4-BasicNetworking.pdf
#### Tema de roles
- Para conectarse a un rol se hace por ssh con el nombre y localhost
#### Cosas de sudo
- sudo [-u usuario] comando
#### Zona de Solaris
- Para ver las zonas disponibles usar **zoneadm list -icv**
- Para acceder usar **zlogin zonita**.
- Para cambiar de usuario **su - elbueno**.
### Syslinux
## Instalacion y configuración de la segunda maquina
### Ubuntu Server
#### Container LXC
- Para ver los containers lxc-ls -f
- Para entrar en uno de ellos hacer lxc-attach -n PruebaContainer
### NetBSD
### Refind
## Instalacion y configuración de la tercera maquina
### Cambiar el Shell por defecto
- useradd -D -s /usr/bin/bash 
### Fedora
### FreeBSD
#### Jail (Jaulita)
- Para inicar la jaula hacer **jexec jaulita /bin/sh**
- En el **jail.conf** esta el archivo de configuracion
```
jaulita {
         path = /usr/jail/JAULILLA;
         mount.devfs;
         host.hostname = jaulita
         ip4.addr = 10.0.2.15;
         interface = le0
         exec.start = "bin/sh /etc/rc";
         exec.stop = "/bin/sh  /etc/rc.shutdown";  
}
```
  

## Creacion de usuarios
- Al crear los usuarios hay que comprobar que con entorno grafico al loggearte  
  cualquier usuario puede   entrar. Si un usuario no entra es por que esta mal creado.
- seq te permite generar varios valores 
- mkpasswd hola : te gerena un hash
- mkpasswd --method=sha523crypt hola
### Ubuntu Server, Fedora y Devuan Linux
- Para devuan es **-m user$i**
- Creacion de los usuarios
```
for i in `seq -w 0 999`; do /usr/sbin/useradd -m -p `mkpasswd --method=yescrypt qwerty$i` user$i; done 
```
### Crear un alias Instaladores (en Devuan) donde varios usuarios pueden admninistrar software
- Modificar el archivo **/etc/sudoers** y añadir:
```

```
### NetBSD
-  Crear de los usuarios
```
for i in `seq -w 0 999`; do /usr/sbin/useradd -m -p `pwhash -s yescrypt qwerty$i` user$i; done 

for i in `seq -w 0 999`; do
    username="user$i"
    password="querty$i"  
    hash=`pwhash yescrypt "$password"`
    useradd -m -d "/home/$username" -p "$hash" "$username"
done
```
### FreeBSD y OpenBSD
- Creacion de los usuarios
``` 
for i in `seq -w 0 999`; do /usr/sbin/useradd -m -p `encrypt -s yescrypt qwerty$i` user$i; done 
```
### Solaris
#### 1. Creacion del archivo users.txt
```
for i in `seq -w 0 999`; do  `echo "user$i qwerty$i" >> users.txt`; done 
```
#### 2. Usar el script pass.expect
```
#!/usr/bin/expect -f

if {$argc!=2} {
   send_user "uso: $argv0 usuario password \n"
   exit
}

set user [lindex $argv 0]
set password [lindex $argv 1]

spawn passwd $user
expect "New Password: "
send "$password\r"
expect "Re-enter new Password: "
send "$password\r"
send "\r"
expect eof
```
#### 3. Creacion del script user.sh
```
#!bin/bash
IFS=$'\n'
contras = `cat /export/home/usuario/users.txt`
for i in $contras
do
a1=$(echo $i | awk '{print $1}')
useradd -m $a1
a2=$(echo $i | awk '{print $2}')
/usr/bin/expect -f pass.expect $a1 $a2
done 
```
#### Crecion del rol Instalador para instalar y elmininar Software
- Creacion del rol
```
roleadd -c "Administrador de software" -s /usr/bin/pfbash -m -K profiles="Software Installation" Instalador
```
- Asignar contraseña al rol 
```
passwd Instalador
```
- Asignar los roles al usuario y probar
```
usermod -R +Instalador user100
```
```
su Instalador
```

#### Hacer que los usuarios user444. user555 y user666 junto con usuario puedan hacerse root
```
usermod -R +root user444
```
#### 

### Establecer fecha de caducidad a un usuario
- En solaris hay que ir al /etc/shadows y añadir en el 2º campo empezando por la derecha la fecha.  
  Para el 8 de abril de 2023 es 19455
```
usermod -e 2023-04-08 user100
```
## Borrado de usuarios
```
for i in `seq -w 0 999`; do /usr/sbin/userdel -r user$i; donels
```
## Asignacion de las contraseñas
```
  for i in `seq -w 0 999`; do
    username="user$i"
    echo -e "user24\nuser24" | sudo passwd $username;
done
```
