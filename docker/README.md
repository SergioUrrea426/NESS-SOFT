# Docker Compose - Base de Datos PostgreSQL

## Descripción
Este archivo `docker-compose.yml` configura un contenedor de PostgreSQL para el proyecto Valkiria System con la siguiente información:

- **Base de Datos**: ness_soft
- **Usuario**: ness_soft
- **Contraseña**: 1234
- **Puerto**: 5432
- **Imagen**: postgres:15

## Requisitos Previos
Asegúrate de tener instalado:
- [Docker](https://www.docker.com/products/docker-desktop)
- [Docker Compose](https://docs.docker.com/compose/install/)

## Instrucciones de Uso

### 1. Iniciar el Compose de Docker

Navega a la carpeta donde está el archivo `docker-compose.yml`:

```bash
cd C:\\Users\\Sergio\\JavaProyect\\valkiria-system\\infrastructure\\docker
```

Luego ejecuta el siguiente comando para iniciar los servicios:

```bash
docker-compose up -d
```

El parámetro `-d` ejecuta los contenedores en segundo plano (detached mode).

### 2. Verificar que la Base de Datos está Funcionando

Para verificar que el contenedor de PostgreSQL está corriendo correctamente:

```bash
docker-compose ps
```

Deberías ver algo como:
```
NAME          COMMAND                  SERVICE      STATUS
ness_soft_db  "docker-entrypoint.s…"   postgres     Up (healthy)
```

### 3. Conectarse a la Base de Datos

Puedes conectarte a la base de datos usando cualquier cliente de PostgreSQL (DBeaver, pgAdmin, etc.) con los siguientes datos:

- **Host**: localhost
- **Puerto**: 5432
- **Base de Datos**: ness_soft
- **Usuario**: ness_soft
- **Contraseña**: 1234

O desde la línea de comandos usando `psql`:

```bash
psql -h localhost -U ness_soft -d ness_soft
```

### 4. Ver los Logs del Contenedor

Para ver los logs en tiempo real:

```bash
docker-compose logs -f postgres
```

Para salir de los logs, presiona `Ctrl + C`.

### 5. Detener los Servicios

Para detener los contenedores sin eliminarlos:

```bash
docker-compose stop
```

Para detener y eliminar los contenedores:

```bash
docker-compose down
```

Para detener, eliminar los contenedores y también los volúmenes (esto eliminará los datos de la base de datos):

```bash
docker-compose down -v
```

### 6. Reiniciar los Servicios

Para reiniciar los servicios:

```bash
docker-compose restart
```

## Notas Importantes

- El volumen `postgres_data` persiste los datos de la base de datos incluso cuando se detienen los contenedores.
- La red `ness_soft_network` permite que otros servicios del proyecto se comuniquen con la base de datos.
- El health check verifica automáticamente que PostgreSQL esté listo para aceptar conexiones.

## Solución de Problemas

### Puerto 5432 ya está en uso
Si el puerto 5432 ya está en uso, puedes cambiarlo en el archivo `docker-compose.yml`:
```yaml
ports:
  - "5433:5432"  # Usa el puerto 5433 localmente
```

### Eliminar contenedor corrupto
Si el contenedor de PostgreSQL está corrupto, ejecuta:
```bash
docker-compose down -v
docker-compose up -d
```

### Ver detalles del contenedor
```bash
docker inspect ness_soft_db
```


### Finalizar Procesos En El Puerto Windows
```bash/cmd
Primero buscas el puero con el siguiente comando
netstat -ano | findstr :[PUERTO]

[PUERTO] esto lo remplazar por el numero del puerto ej: 5432

En el resultado sacamos el numero PID(este sale en la ultima columna de la derecha) luego ejecutas este comando:
taskkill /PID [PID] /F

[PID] esto lo remplazas por el numero  PID ej: 9596

Ya con eso puedes ejecutar de nuevo el comando de docker-compose up -d
```
