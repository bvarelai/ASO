# Administración básica de la red
## Importante
- Comando dladm shon-phys
- Configurar dos tarjetas de red en 192.168.1 192.168.10 162.168.100 : Cada tarjeta en cada operativo tiene 3 ips
-  La segunda y tercera tarjeta seria igual pero .2 .20 .200
-  Dar de alta en /etc.host a las tarjetas con nombres rollo aso1-1,aso1-2
-  Debian y derivados : /etc/network/interfaces
-  Fedora : /etc/sysconfig/network-scripts/ifcfg-nombre de la tarjeta  
-  Solaris : se usa el comando ipadm para crear las tarjetas de red
-  En Solaris hay que configurar init.d para poder usar sshd
## Configuracion de la primera máquina
### Devuan
### OpenBSD
### Solaris
## Configuracion de la segunda máquina
### Ubuntu Server
### NetBSD
## Configuracion de la tercera máquina
### Fedora
- Ir al directorio `/etc/sysconfig/network-scripts/` y crear una serie de archivos:  

Archivo `ifcfg-enp0s3`
```
DEVICE=enp0s3
BOOTPROTO=dhcp
ONBOOT=yes
NM_CONTROLLED=no
HWADDR=08:00:27:78:96:88
```
Archivo `ifcfg-enp0s8`
```
DEVICE=enp0s8
BOOTPROTO=none
IPADDR=192.168.1.103
NETMASK=255.255.255.0
BROADCAST=192.168.1.255
IPADDR=192.168.10.103
NETMASK=255.255.255.0
IPADDR=192.168.100.103
NETMASK=255.255.255.0
NM_CONTROLLED=no
HWADDR=08:00:27:1a:bd:db
ONBOOT=yes
```
Archivo `ifcfg-enp0s9`
```
DEVICE=enp0s9
BOOTPROTO=none
IPADDR=192.168.2.103
NETMASK=255.255.255.0
BROADCAST=192.168.2.255
IPADDR=192.168.20.103
NETMASK=255.255.255.0
IPADDR=192.168.200.103
NETMASK=255.255.255.0
NM_CONTROLLED=no
HWADDR=08:00:27:de:43:1e
ONBOOT=yes
```

### FreeBSD
- Ir al archivo `/etc/rc.conf ` y añadir las siguientes lineas:
```
ifconfig_em0="DHCP"
ifconfig_em1="inet 192.168.1.103 netmask 255.255.255.0"
ifconfig_em2="inet 192.168.2.103 netmask 255.255.255.0"
ifconfig_em1_alias0="inet 192.168.10.103 netmask 255.255.255.0"
ifconfig_em1_alias1="inet 192.168.100.103 netmask 255.255.255.0"
ifconfig_em2_alias0="inet 192.168.20.103 netmask 255.255.255.0"
ifconfig_em2_alias1="inet 192.168.200.103 netmask 255.255.255.0"
```
- Esta configuracion es persistente, por lo que se mantendra tras un reinicio de la maquina.
  


