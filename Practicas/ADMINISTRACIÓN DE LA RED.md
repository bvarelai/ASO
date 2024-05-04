# Administración básica de la red
## Importante
- Comando dladm shon-phys
- Configurar dos tarjetas de red en 192.168.1 192.168.10 162.168.100 : Cada tarjeta en cada operativo tiene 3 ips
-  La segunda y tercera tarjeta seria igual pero .2 .20 .200
-  Dar de alta en `/etc.hosts` a las tarjetas con nombres rollo aso1-1,aso1-2
```
192.168.1.101  aso1-1
192.168.2.101  aso1-2

192.168.1.102  aso2-1
192.168.2.102  aso2-2

192.168.1.103  aso3-1
192.168.2.103  aso3-2
```

-  Debian y derivados : /etc/network/interfaces
-  Fedora : /etc/sysconfig/network-scripts/ifcfg-nombre de la tarjeta  
-  Solaris : se usa el comando ipadm para crear las tarjetas de red
-  En Solaris hay que configurar init.d para poder usar sshd
## Configuracion de la primera máquina
### Devuan
- Ir al directorio /etc/network/interfaces y añadir:
```
# This file describes the network interfaces available on your system
# and how to activate them. For more information, see interfaces(5).

source /etc/network/interfaces.d/*

# The loopback network interface
auto lo
iface lo inet loopback

# The primary network interface
auto eth0
allow-hotplug eth0
iface eth0 inet dhcp

# The secondary network interface
auto eth1
iface eth1 inet static 
address 192.168.1.101 
netmask 255.255.255.0
network 192.168.1.0
broadcast 192.168.1.255
gateway 192.168.1.1

auto eth1:0
iface eth1:0 inet static
address 192.168.10.101

auto eth1:1
iface eth1:1 inet static
address 192.168.100.101

# The third network interface
auto eth2
iface eth2 inet static
address 192.168.2.101
netmask 255.255.255.0
network 192.168.2.0  
broadcast 192.168.2.255
gateway 192.168.2.1  

auto eth2:0
iface eth2:0 inet static
address 192.168.20.101

auto eth2:1
iface eth2:1 inet static
address 192.168.200.101
```
### OpenBSD
- Crear los siguientes archivos:
  
Archivo `/etc/hostname.em0`  
```
inet autoconf
```
Archivo `/etc/hostname.em1`
```
inet 192.168.1.101 255.255.255.0
inet alias 192.168.10.101 255.255.255.255
inet alias 192.168.100.101 255.255.255.255
```
Archivo  `/etc/hostname.em2`  
```
inet 192.168.2.101 255.255.255.0
inet alias 192.168.20.101 255.255.255.255
inet alias 192.168.200.101 255.255.255.255
```
### Solaris
- Utilizar los siguientes comandos:
Crear la interfaz `net0` por dhcp y las `net1` y `net2` con IP propias
```
ipadm create-ip net0
ipadm create-addr -T dhcp net0/addr
ipadm create-ip net1
ipadm create-addr -T static -a 192.168.1.101/24 net1/addr
ipadm create-ip net2
ipadm create-addr -T static -a 192.168.2.101/24 net2/addr
```


## Configuracion de la segunda máquina
### Ubuntu Server
- Ir al mismo fichero que el Devuan y poner lo siguiente:
```
# interfaces(5) file used by ifup(8) and ifdown(8)
# Include files from /etc/network/interfaces.d:
source /etc/network/interfaces.d/*

# The loopback network interface
auto lo
iface lo inet loopback


# The primary network interface
auto enp0s3
allow-hotplug enp0s3
iface enp0s3 inet dhcp


# The second network interface
#auto enp0s8
iface enp0s8 inet static 
address 192.168.1.101 
netmask 255.255.255.0
network 192.168.1.0
broadcast 192.168.1.255
gateway 192.168.1.1

#auto enp0s8:0
iface enp0s8:0 inet static
address 192.168.10.101

#auto enp0s8:1
iface enp0s8:1 inet static
address 192.168.100.101


# The third network interface
#auto enp0s9
iface enp0s9 inet static
address 192.168.2.101
netmask 255.255.255.0
network 192.168.2.0  
broadcast 192.168.2.255
gateway 192.168.2.1  

#auto enp0s9:0
iface enp0s9:0 inet static
address 192.168.20.101

#auto enp0s9:1
iface enp0s9:1 inet static
address 192.168.200.101
```
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
  


