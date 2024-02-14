# Tema 2 : Arranque e Instalacion de Sistemas
## Proceso de Arranque
### Fases
- **Firmware** : referente al arranque (puede ser BIOS o UEFI)
- **Cargador** : carga el Kernel en el SO
- **El Kernel** : Coge el Hardware y crea un proceso (Init)
- **Scripts (Init)** : Init coge los scripts y los ejecuta ( iniciando el resto)
##### BIOS VS UEFI
- En **UEFI** el arranque esta en el fichero de disco (entiende el sistema de ficheros)
- El **BIOS** no tiene el fichero en disco (no entiende lo que es un fichero y por tanto lo que es un sistema de ficheros). Este solamente lanza el primer bloque del disco(el **Cargador**, que puede estar en el primer bloque de la partición o del disco)
