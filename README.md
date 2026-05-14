# Backend Despachos — Innovatech Chile

API REST desarrollada con Spring Boot para la gestión de despachos de Innovatech Chile. Desplegada en contenedores Docker sobre AWS EC2.

## Tecnologías

- Java 17
- Spring Boot 3.4.4
- MySQL 8.0
- Docker + Docker Compose
- GitHub Actions (CI/CD)

## Estructura del proyecto
back-Despachos_SpringBoot/
├── .github/
│   └── workflows/
│       └── deploy.yml        # Pipeline CI/CD
└── Springboot-API-REST-DESPACHO/
├── Dockerfile             # Multi-stage build
├── docker-compose.yml     # Stack completo con MySQL
└── src/                   # Código fuente

## Variables de entorno requeridas

| Variable | Descripción |
|---|---|
| DB_ENDPOINT | Host de la base de datos |
| DB_PORT | Puerto MySQL (3306) |
| DB_NAME | Nombre de la base de datos |
| DB_USERNAME | Usuario de la base de datos |
| DB_PASSWORD | Contraseña de la base de datos |

## Correr localmente con Docker

```bash
cd Springboot-API-REST-DESPACHO
docker compose up --build
```

La API quedará disponible en `http://localhost:8081`

Documentación Swagger: `http://localhost:8081/swagger-ui.html`

## Pipeline CI/CD

El pipeline se activa automáticamente al hacer push a la rama `deploy`:

1. Construye la imagen Docker con multi-stage build
2. Publica la imagen en Docker Hub
3. Despliega automáticamente en la instancia EC2

## Persistencia de datos

Se utiliza un **named volume** (`despachos_mysql_data`) para persistir los datos de MySQL. Se eligió named volume sobre bind mount porque en entornos EC2 no se conoce la ruta exacta del host, y Docker gestiona el volumen de forma independiente.
