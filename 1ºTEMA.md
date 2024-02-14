# Evaluacion
## Examen Final
- **4 puntos** : Examen final
## Practicas y Trabajos
- **4 puntos** : 2 puntos de un examen de practicas y 2 puntos de practicas.
- **2 puntos** : Exponer un trabajo frente a varios personas o corregir el trabajo de otros (justificando).
Se puede conservar cualquier parte para el año que viene.
## Web con los apuntes
- **URL** : https://www.dc.fi.udc.es/~afyanez/Docencia/index.html
Detras de la "a" va la virgulilla
# Tema 1 : Introducción
## Que es un Administrador de Sistemas
El administrador de sistema es quien da privilegios a los usuarios, de manera que puede restringir cosas.
Se ocupa de la instalacion,configuracion, mantenimiento y seguridad del sistema.
Nunca debes tener directamente privilegios de administrador como usuario.
## Usuarios
Roles (usuarios ficticios)
Todos los usuarios que esten en "sudoers" pueden usar el comando sudo.
- **su** : Me pone en modo superusuario pero me quedo en el directorio en el que estaba.
- **su -** : Lo mismo pero me lleva al /root.
- **su - visita** : Me meto al usuario visita.
- **/bin** : Ejecutables esenciales
- **/usr/bin** : Ejecutables no esenciales
- **/sbin** : Binarios esenciales
- **/usr/sbin** : Binarios no esenciales
- **Autentificacion** : Le digo a la maquina que soy quien digo ser
- **Pseudousuarios** : Usuarios que ejecutan servicios especificos
Los directorios se asocian a un usuario por el numero de usuario (el 1004 por ejemplo)
Tengo un directorio asociado a un usuario con ese numero, si borro el usuario sin borrar el directorio
y creo un usuario nuevo (que no tiene directorio) se asociaria al directorio anterior en el caso de que tenga el 1004,
ya que ese directorio esta asociado al numero 1004
## Manual(comando man)
### Comandos
- man -k user : Buscar por letra.
- man 3 printf : Te busca en las seccion 3 del manual lo relacionado con printf.
- man -k user | grep add : Busca todo lo relacionado con añadir usuarios.
### Aclaración
Al principio, cuando se inicia la maquina el man -k no va a funcionar ya que usa indices.
Por ello deben generarse los indices( en algunos sistemas se ponen mandb o kadman o mandoc)
IMPORTANTE : Cada cambio (hacerlos de uno en uno y que sean reversibles) que hagas comprobar que todo funciona. Testear antes de ejecutar.
Para comprobar que el script funciona bien se puede poner un echo en las lineas que se van a ejecutar para ver lo que harian.
## Grupos
- **Grupo staff** : Grupo por defecto donde meto a los usuarios que creo.
Puedo meterlos en otro grupo si lo indico.
El usuario puede pertencer a varios grupos pero uno sera el primario, que esta definido en el fichero /etc/passwd.
Los ficheros creados en un directorio son del grupo de ese directorio.
### En /etc/passwd
- nombre_usuario:x:nº_usuario:nº_grupo
## Permisos
- Permiso de **ejecucion** : Entrar en un directorio
- Permiso de **lectura/escritura** : Leer o modificar un directorio
sticky bit : la t del final. Impide poder borrar un directorio si no eres el dueño, aunque tengas permisos de escritura sobre el.
## Procesos
- Exceptuando el proceso con PID 1 (el systemd) y otros procesos del arranque, todos los procesos son creados por otros proceso (proceso  padre).Los procesos se terminan con exit()
### Tipos
- **Interactivos** : Estos tienen un terminal de control (Ejemplo: comando vi). El valor TT del proceso te lo dice
- **No Interactivos** : No estan asociados a ninguna terminal de control. No tiene valor TT, o es nulo (creo)
- **Daemons** : Proceso no interactivo que tiene la palabra de daemon en el nombre y se usa start-stop-daemon para iniciar y parar.   (Ejemplo: el log)
## Variables de entorno
- Con **echo $PATH** se nos muestra los lugares donde se guardarian las variables de entorno (en orden)
- Para debian se hace **su -** (**su** no sirve) ya que en Debian no existen /usr/sbin ni /sbin
## Señales
Un proceso ante una señal puede: Finalizar, ignorarla o captar la señal y hacer una accion.
### Tipos
- **HUP(hangup)** : Señal para indicar que se termine el proceso
- **STOP** : Parar el proceso
- **CONT** : Continuar el proceso
- **KILL** : Matar el proceso
## Comandos de Administracion
### Vi
- Se inserta con **i** y se concatena con **a**. Estos dos comandos te permiten pasar del modo comando al modo texto
- Con **escape** sales del modo texto y vuelves al modo comando.


