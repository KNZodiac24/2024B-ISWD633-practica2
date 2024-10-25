### Crear contenedor de Postgres sin que exponga los puertos. Usar la imagen: postgres:11.21-alpine3.17
```
docker run -d --name postgres -e POSTGRES_PASSWORD=admin postgres:11.21-alpine3.17
```

### Crear un cliente de postgres. Usar la imagen: dpage/pgadmin4
```
docker run -d --name pgadmin -p 82:80 -e PGADMIN_DEFAULT_EMAIL=admin@admin.admin -e PGADMIN_DEFAULT_PASSWORD=admin dpage/pgadmin4
```

La figura presenta el esquema creado en donde los puertos son:
- a: 5432
- b: 80
- c: 82

![Imagen](img/esquema-ejercicio3.PNG)

## Desde el cliente
### Acceder desde el cliente al servidor postgres creado.
![Login pgadmin](img/login_pgadmin.png)
![dash_pgadmin](img/dash_pgadmin.png)

### Crear la base de datos info, y dentro de esa base la tabla personas, con id (serial) y nombre (varchar), agregar un par de registros en la tabla, obligatorio incluir su nombre.

## Desde el servidor postgresl
### Acceder al servidor
### Conectarse a la base de datos info
```
docker exec -it postgres psql -U postgres -d info
```

### Realizar un select *from personas
![Consulta postgres](img/postgres_tabla.png)
