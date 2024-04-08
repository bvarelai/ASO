# Tema 4: Administracion de usuarios
## Usuarios
- Se identifican por un numero (uid), no por su nombre.
- Hay un usuario especial (uid=0 , el root) en el sistema que puede acceder a todos los ficheros, hacer todas las llamadas
  al sistema y lanzar señales a procesos.
- Un fichero pertence a un solo usuario y grupo. El grupo del que pertenece el fichero puede ser un grupo en el
  que usuario no pertenezca.
## Grupo
- Se identifican por un numero (guid), no por el nombre.
- Un usuario puede pertenecer a varios grupos y un grupo puede tener varios usuarios.
- Uno de esos grupos se conoce como el grupo primario.
