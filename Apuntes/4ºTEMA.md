# Tema 4: Administracion de usuarios
## Usuarios
- Se identifican por un numero (uid), no por su nombre.
- Hay un usuario especial (uid=0 , el root) en el sistema que puede acceder a todos los ficheros, hacer todas las llamadas al sistema y lanzar señales a procesos.
- Un fichero pertence a un solo usuario y grupo. El grupo del que pertenece el fichero puede ser un grupo en el
  que usuario no pertenezca.
## Grupo
- Se identifican por un numero (guid), no por el nombre.
- Un usuario puede pertenecer a varios grupos y un grupo puede tener varios usuarios.
- Uno de esos grupos se conoce como el grupo primario.
- En los sistemas BSD los ficheros pertencen al grupo asociado al directorio en el que estan.
## Ficheros de la base de datos de usuarios
- La informacion de los usuarios se almacena en ficheros de texto, estos se localizan en /etc.
- Dentro de /etc/ tenemos:
- /etc/passwd : cuentas de usuario
- /etc/shadow : passwd de usuarios (linux)
- /etc/group : grupos
- /etc/gshadow/ : passwd de grupos
- /etc/master.passwd/: cuentas de usuarios y contraseñas (BSD)
- En /etc/passwd cada linea representa un usuario.
  **username:x:UID:GID:user information:home-directory:login-shell**  
  **x**: como se encripta la password  
  **login-shell**: el interprete usado  
- En /etc/shadow solo de escritura y lectura para el root, tiene la informacion de las passwords
  **username:password:lastchg:min:max:warn:inactive:expire:reserved**  
  **lastchg**: la ultima vez(fecha) que se cambio la contraseña   
  **min**: minimo numero de dias que se requieren para cambiar la contraseña  
  **max**: numero maximo de dias que la passwd es valida  
  **warn**: numero dias antes de que expire el usuario es avisado  
  **inactive**: dias que la passwd se aceptara despues de que esta expirara  
  **expire**: dia que la cuenta expira  
  **reserved**: para uso futuro
## Shell Reducidos
- Shell en el que no puedes modificar variables de entorno y tocar el PATH. Creas un directorio  
y en ese olo puedes hacer una serie de comandos
- login class se encuentra en /etc/login.conf. Tambien esta la default class. 
## PAM
- Este es un programa de login, provee una libreria de funciones que se pueden usar para comprobar que el usuario esta autenticado.  
### Modulos
- sufficient : si el modulo PAM dice que si, es que si. Si dice no, no pasa nada.  
- requisite: si el modulo dice que no, es que no. Si dice si nada.  
