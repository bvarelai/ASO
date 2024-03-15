# Tema 2 : Arranque e Instalacion de Sistemas
## Proceso de Arranque
### Fases
- **Firmware** : referente al arranque (puede ser BIOS o UEFI)
- **Cargador** : carga el Kernel en el SO
- **El Kernel** : Coge el Hardware y crea un proceso (Init)
- **Scripts (Init)** : Init coge los scripts y los ejecuta ( iniciando el resto)
#### BIOS VS UEFI
- En **UEFI** el arranque esta en el fichero de disco (entiende el sistema de ficheros)
- El **BIOS** no tiene el fichero en disco (no entiende lo que es un fichero y por tanto lo que es un sistema de ficheros). Este solamente lanza el primer bloque del disco(el **Cargador**, que puede estar en el primer bloque de la partición o del disco)
#### Firmware
- En el caso de particiones MBR el cargador se coloca en el primer bloque de la particion activa
##### Tipo BIOS

##### Tipo UEFI
- Puedes tener dos particiones de tipo UEFI (ESP las dos)
- Para poder varios sistemas operativos ,hacer chainload o cambiar la particion activa. Este va a arrancar el fichero /EFI/BOOT/BOOTX64.EFI, que es el cargador. Este se puede poniendo otro (cambiar el orden)

