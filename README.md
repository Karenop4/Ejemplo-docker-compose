# Ejemplo Docker Compose - Users Service

Este proyecto es un microservicio de usuarios construido con **NestJS** y **PostgreSQL**, orquestado completamente con **Docker Compose**.

## Requisitos Previos

- **Docker**: [Descargar Docker Desktop](https://www.docker.com/products/docker-desktop)
- **Docker Compose**: (incluido con Docker Desktop)
- **Git** (para clonar el repositorio)

Para verificar Docker instalado correctamente:

```bash
docker --version
docker-compose --version
```

## Ejecutar el Proyecto Completo

Desde la raíz del proyecto, ejecutar:

```bash
docker-compose up --build
```

Este comando:
- **Construirá** la imagen de Docker para el servicio de usuarios
- **Levantará** el servicio de usuarios en el puerto `3000`
- **Levantará** la base de datos PostgreSQL en el puerto `5432`
- **Creará** los volúmenes necesarios para persistencia de datos

## Estructura del Proyecto

```
ejemplo_docker_compose/
├── docker-compose.yaml       # Orquestación de servicios
├── README.md                 # Este archivo
└── users-service/            # Microservicio NestJS
    ├── Dockerfile            # Imagen Docker multi-stage
    ├── package.json          # Dependencias Node
    ├── tsconfig.json         # Configuración TypeScript
    ├── src/                  # Código fuente
    │   ├── main.ts
    │   ├── app.module.ts
    │   └── user/
    │       ├── user.controller.ts
    │       ├── user.service.ts
    │       ├── user.entity.ts
    │       ├── user.module.ts
    │       └── dto/
    │           └── create-user.dto.ts
    └── test/                 # Tests
```

## Servicios Incluidos

### Users Service
- **Framework**: NestJS 10
- **Lenguaje**: TypeScript
- **Puerto**: `3000`
- **Base de Datos**: PostgreSQL (internas)
- **Estado**: Accesible en `http://localhost:3000`

### PostgreSQL Database
- **Versión**: 15
- **Puerto**: `5432`
- **Usuario**: `user`
- **Contraseña**: `pass`
- **Base de Datos**: `usersdb`
- **Volumen Persistente**: `db-data`

## Detener los Servicios

Para detener todos los servicios:

```bash
docker-compose down
```

Para detener y eliminar volúmenes (incluyendo datos de la BD):

```bash
docker-compose down -v
```

## Comandos

### Ver logs de un servicio específico
```bash
docker-compose logs users-service
docker-compose logs db
```

### Logs en tiempo real
```bash
docker-compose logs -f users-service
```

### Verificar estado de servicios
```bash
docker-compose ps
```

### Acceder a la terminal del contenedor
```bash
docker-compose exec users-service sh
docker-compose exec db psql -U user -d usersdb
```

## Conectar a PostgreSQL

Desde el cliente SQL o la terminal:

```bash
Host: localhost
Puerto: 5432
Usuario: user
Contraseña: pass
Base de Datos: usersdb
```

O usando `psql` desde terminal:

```bash
psql -h localhost -U user -d usersdb
```

## Build Dockerfile

El proyecto usa un **Dockerfile multi-stage**:

1. **Etapa de Build**: Compila el código TypeScript
2. **Etapa de Runtime**: Ejecuta solo la aplicación compilada (imagen más ligera)

## Variables de Entorno

El proyecto espera un archivo `.env` en `users-service/`. Con las variables necesarias para conectar a PostgreSQL.
 
`.env`:
```
DATABASE_HOST=db
DATABASE_PORT=5432
DATABASE_USER=user
DATABASE_PASSWORD=pass
DATABASE_NAME=usersdb
```

## Recursos Adicionales

- [Documentación Docker Compose](https://docs.docker.com/compose/)
- [Documentación NestJS](https://docs.nestjs.com/)
- [Documentación TypeORM](https://typeorm.io/)
- [Documentación PostgreSQL](https://www.postgresql.org/docs/)

---
    
