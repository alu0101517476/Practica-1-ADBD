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

![nombre](img/admin_biblio.png)

- Crear un usuario **usuario_biblio** con permisos solo de lectura.  



### Creación de roles
- Crear un rol llamado **lectores** con permisos únicamente de consulta sobre todas las tablas de la base de datos.  

### Asignación de roles
- Asignar el usuario **usuario_biblio** al rol **lectores**.  

### Consulta de usuarios
- Consultar las tablas del sistema para listar todos los usuarios creados (`pg_roles`).  

### Cambio de contraseña
- Cambiar la contraseña del usuario **usuario_biblio**.  

### Restricciones de permisos
- Configurar permisos de tal forma que el usuario **usuario_biblio** no pueda eliminar registros en ninguna tabla.  

---

## Creación de Tablas
- Crear la tabla **autores** con los campos:  
  - `id_autor` (clave primaria)  
  - `nombre`  
  - `nacionalidad`  


