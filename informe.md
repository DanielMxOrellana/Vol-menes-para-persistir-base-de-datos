# Práctica No. 3 – Contenedor con Base de Datos PostgreSQL en Docker
## 1. Título  
**Persistencia de Datos en Contenedores PostgreSQL con y sin Volúmenes**
## 2. Tiempo de duración
45 Minutos
## 3. Fundamentos  

En esta práctica se busca comprender cómo Docker maneja la persistencia de datos en contenedores que ejecutan bases de datos, específicamente **PostgreSQL**. Docker es una tecnología de virtualización ligera que permite ejecutar aplicaciones en contenedores aislados, los cuales incluyen todo lo necesario para su funcionamiento: sistema base, dependencias y configuraciones.

Por defecto, cuando se elimina un contenedor en Docker, todos los datos almacenados dentro de él también se eliminan, ya que el sistema de archivos del contenedor es efímero. Sin embargo, Docker ofrece una solución para conservar los datos: **los volúmenes**. Los volúmenes permiten almacenar información de manera persistente en el host, independiente del ciclo de vida del contenedor.

PostgreSQL, por su parte, es un sistema gestor de bases de datos relacional de código abierto, ampliamente utilizado por su estabilidad, robustez y soporte a transacciones ACID. En un entorno con Docker, PostgreSQL se ejecuta como una imagen preconfigurada disponible en Docker Hub, la cual se puede desplegar fácilmente con el comando `docker run`.

En esta práctica se realizan dos partes:  
1. Crear un contenedor de PostgreSQL **sin volumen**, verificar la pérdida de datos al eliminarlo.  
2. Crear un contenedor de PostgreSQL **con un volumen persistente**, comprobar que los datos permanecen incluso después de borrar y volver a crear el contenedor.

Estas pruebas permiten entender la diferencia entre los datos **efímeros** (sin volumen) y **persistentes** (con volumen), fundamentales para administrar bases de datos en entornos productivos.

## 4. Conocimientos previos.
   
Para realizar esta práctica necesitamos tener claros los siguientes temas:

- Comandos básicos de **Linux / PowerShell**.  
- Conocimiento básico de **Docker**: contenedores, imágenes, puertos y volúmenes.  
- Instalación y configuración de **Docker Desktop**.  
- Uso de un **administrador gráfico de bases de datos** (TablePlus).  
- Conexión de aplicaciones externas a un contenedor de base de datos

## 5. Objetivos a alcanzar
   
- Implementar contenedores con **PostgreSQL**.  
- Manipular **volúmenes de Docker** para lograr persistencia de datos.  
- Conectarse a la base de datos desde una herramienta gráfica.  
- Comprobar el comportamiento de los datos al eliminar y recrear contenedores.
  
## 6. Equipo necesario:
  
- Computador con sistema operativo Windows
- Docker Desktop v28.5.1 o superior.  
- Acceso a internet (para descargar imágenes desde Docker Hub).  
- TablePlus 
- Cuenta en Docker Hub.  


## 7. Material de apoyo.
   
- [Documentación oficial de Docker](https://docs.docker.com)  
- [Documentación oficial de PostgreSQL](https://www.postgresql.org/docs/)  
- Guía de asignatura de virtualización y contenedores.  
- Linux cheat sheet – comandos básicos.  

  
## 8. Procedimiento

### Parte 1: Base de datos sin volumen  

**Paso 1.** Crear el contenedor PostgreSQL:  

docker run --name server_db1 -e POSTGRES_PASSWORD=mysecretpassword -e POSTGRES_USER=postgres -p 5432:5432 -d postgres:15 
Paso 2. Verificar que el contenedor está corriendo:
docker ps
![alt text](<Parte 1 — Base de datos sin volumen (los datos se pierden).png>)
Paso 3. Crear una base de datos test y una tabla customer
![alt text](<Crear la base de datos test, la tabla customer e insertar un registro.png>)
Paso 4. Detener y eliminar el contenedor:
![alt text](<Volver a crear el contenedor con el mismo comando (sin volumen).png>)
Paso 5. Conectarse desde TablePlus o pgAdmin con los parámetros:
![alt text](<Captura de pantalla 2025-10-23 145428.png>)
![alt text](<Captura de pantalla 2025-10-23 145406.png>)
Parte 2: Base de datos con volumen

Paso 1. Crear un volumen llamado pgdata:
![alt text](<Parte 2 — Base de datos con volumen (los datos persisten).png>)
Paso 2. Crear el contenedor PostgreSQL con volumen:
![alt text](<Crear el contenedor server_db2 montando el volumen (usamos puerto 5433 en host para evitar choque).png>)
Paso 4. Detener y eliminar el contenedor:
Paso 5. Volver a crear el contenedor con el mismo volumen:
![alt text](<Captura de pantalla 2025-10-25 083741.png>)
## 9. Resultados esperados:
    
En la Parte 1, al eliminar el contenedor, la base de datos test desaparece.

En la Parte 2, al usar el volumen pgdata, los datos permanecen tras eliminar y recrear el contenedor.

Se comprueba el uso de volúmenes para garantizar persistencia de datos en entornos Docker.

## 10. Bibliografía
    
Docker Inc. (2024). Docker Documentation. Recuperado de https://docs.docker.com

PostgreSQL Global Development Group. (2024). PostgreSQL Documentation. Recuperado de https://www.postgresql.org/docs/

PhoenixNAP. (2021). How to Use Docker Volumes. Recuperado de https://phoenixnap.com/kb/docker-volumes

Cyberciti.biz. (2021). Docker persistent data storage tutorial.
