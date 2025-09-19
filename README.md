# Practica-1-ADBD
### Autores: Eric Bermúdez Hernández
###          Alba Pérez Rodríguez


## Índice
1. [Introducción](#introducción)  
2. [Creación de la Base de Datos](#creación-de-la-base-de-datos)  
3. [Gestión de Usuarios y Roles](#gestión-de-usuarios-y-roles)  
   - [Creación de usuarios](#creación-de-usuarios)  
   - [Creación de roles](#creación-de-roles)  
   - [Asignación de roles](#asignación-de-roles)  
   - [Consulta de usuarios](#consulta-de-usuarios)  
   - [Cambio de contraseña](#cambio-de-contraseña)  
   - [Restricciones de permisos](#restricciones-de-permisos)  
4. [Creación de Tablas](#creación-de-tablas)  

---

## Introducción


---


## Creación de la Base de Datos

``` sql
create database biblioteca;
``` 


---


## Gestión de Usuarios y Roles

### Creación de usuarios
- Crear un usuario **admin_biblio** con permisos de administrador sobre la base de datos.  

![admin_biblio creado](img/admin_biblio.png)

- Crear un usuario **usuario_biblio** con permisos solo de lectura.  
*ERIC:*
```sql
CREATE USER usuario_biblio;
GRANT USAGE ON SCHEMA public TO usuario_biblio;
ALTER DEFAULT PRIVILEGES IN SCHEMA public
GRANT SELECT ON TABLES TO usuario_biblio;
``` 

**Captura de demostración que el usuario_biblio solo tiene permisos de lectura:**
![usuario_biblio solo lectura](img/usuario_biblio%20lectura.png)

**Explicación:**
Según la consulta realizada en la vista information_schema.role_table_grants, el usuario usuario_biblio no presenta ningún privilegio asignado sobre las tablas de la base de datos. Esto significa que actualmente no puede ejecutar operaciones de lectura ni de escritura. Por tanto, no se le pueden atribuir permisos de solo lectura, ya que en realidad no dispone de acceso alguno a los objetos de la base de datos.


### Creación de roles
- Crear un rol llamado **lectores** con permisos únicamente de consulta sobre todas las tablas de la base de datos.  

```sql

CREATE ROLE lectores;
GRANT CONNECT ON DATABASE biblioteca TO lectores;
GRANT USAGE ON SCHEMA public TO lectores;
GRANT SELECT ON ALL TABLES IN SCHEMA public TO lectores;
ALTER DEFAULT PRIVILEGES IN SCHEMA public GRANT SELECT ON TABLES TO lectores;

```


### Asignación de roles
- Asignar el usuario **usuario_biblio** al rol **lectores**.  

```sql
GRANT lectores TO usuario_biblio;
```

### Consulta de usuarios
- Consultar las tablas del sistema para listar todos los usuarios creados (`pg_roles`).  

```sql
SELECT *
FROM pg_roles;

```
![consulta pg_roles](img/consulta_pg_roles.png)

### Cambio de contraseña
- Cambiar la contraseña del usuario **usuario_biblio**.  

```sql
ALTER USER usuario_biblio WITH PASSWORD '1234';

```
![Cambio contraseña](img/Cambio_contrasenia.png)


### Restricciones de permisos
- Configurar permisos de tal forma que el usuario **usuario_biblio** no pueda eliminar registros en ninguna tabla.  

El usuario usuario_biblio ha sido configurado con permisos exclusivamente de lectura sobre la base de datos biblioteca. Esto se logró concediéndole la capacidad de conectarse a la base de datos, de acceder al esquema público donde se encuentran las tablas y de ejecutar únicamente consultas de tipo SELECT sobre todas las tablas existentes. Además, se configuró de manera que cualquier tabla que se cree en el futuro también le permita únicamente la lectura de datos. Como resultado, usuario_biblio puede consultar toda la información de la base de datos, pero cualquier intento de modificar, insertar o eliminar registros será denegado automáticamente, garantizando que este usuario cumpla estrictamente con la restricción de no poder eliminar registros en ninguna tabla.

---

## Creación de Tablas
- Crear la tabla **autores** con los campos:  
  - `id_autor` (clave primaria)  
  - `nombre`  
  - `nacionalidad`  


