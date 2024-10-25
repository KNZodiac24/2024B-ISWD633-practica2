# Variables de Entorno
### ¿Qué son las variables de entorno?

Son variables dinámicas que se definen en el sistema operativo y pueden afectar el comportamiento de las aplicaciones y los procesos en ejecución en el equipo.

### Para crear un contenedor con variables de entorno

```
docker run -d --name <nombre contenedor> -e <nombre variable1>=<valor1> -e <nombre variable2>=<valor2>
```

### Crear un contenedor a partir de la imagen de nginx:alpine con las siguientes variables de entorno: username y role. Para la variable de entorno rol asignar el valor admin.
```
docker run -d --name nginx -e username=kenny -e role=admin nginx:alpine
```
![Variables de entorno nginx](img/var_ent_nginx.png)

### Crear un contenedor con mysql:8 , mapear todos los puertos
```
docker run -P -d --name mysql mysql:8 
```

### ¿El contenedor se está ejecutando?

Al ejecutar el comando `docker ps` no se observa al contenedor en ejecución.

### Identificar el problema

Ejecutando `docker logs mysql` se menciona que faltan especificar algunas variables de entorno para el contenedor.

### Eliminar el contenedor creado con mysql:8 
```
docker rm mysql
```

### Para crear un contenedor con variables de entorno especificadas
- Portabilidad: Las aplicaciones se vuelven más portátiles y pueden ser desplegadas en diferentes entornos (desarrollo, pruebas, producción) simplemente cambiando el archivo de variables de entorno.
- Centralización: Todas las configuraciones importantes se centralizan en un solo lugar, lo que facilita la gestión y auditoría de las configuraciones.
- Consistencia: Asegura que todos los miembros del equipo de desarrollo o los entornos de despliegue utilicen las mismas configuraciones.
- Evitar Exposición en el Código: Mantener variables sensibles como contraseñas, claves API, y tokens fuera del código fuente reduce el riesgo de exposición accidental a través del control de versiones.
- Control de Acceso: Los archivos de variables de entorno pueden ser gestionados con permisos específicos, limitando quién puede ver o modificar la configuración sensible.

Previo a esto es necesario crear el archivo y colocar las variables en un archivo, **.env** se ha convertido en una convención estándar, pero también es posible usar cualquier extensión como **.txt**.
```
docker run -d --name <nombre contenedor> --env-file=<nombreArchivo>.<extensión> <nombre imagen>
```
**Considerar**
Es necesario especificar la ruta absoluta del archivo si este se encuentra en una ubicación diferente a la que estás ejecutando el comando docker run.

### Crear un contenedor con mysql:8 , mapear todos los puertos y configurar las variables de entorno mediante un archivo
```
docker run -P -d --name mysql --env-file=variables_mysql.txt mysql:8
```
![Variables de entorno mysql](img/var_ent_mysql.png)

### ¿Qué bases de datos existen en el contenedor creado?
```
docker exec -it mysql mysql -uroot -proot123 -e "SHOW DATABASES;"
```
