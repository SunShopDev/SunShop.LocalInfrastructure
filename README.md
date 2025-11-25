# SunShop.LocalInfrastructure

Infraestructura local para el desarrollo de microservicios SunShop utilizando Docker Compose.

> ⚠️ **Nota de Seguridad**: Esta configuración es solo para desarrollo local. Las credenciales por defecto incluidas no deben usarse en producción. Asegúrese de configurar credenciales seguras para entornos de producción.

## Servicios incluidos

### LocalStack (AWS Local)
Simula servicios AWS localmente para desarrollo y pruebas.

| Configuración | Valor |
|---------------|-------|
| **Imagen** | `localstack/localstack:latest` |
| **Container** | `localstack-aws` |
| **Puertos** | `4566:4566`, `4571:4571` |
| **Servicios AWS** | SQS, SNS, CloudWatch |
| **Región** | `us-east-1` |
| **Access Key** | `test` |
| **Secret Key** | `test` |

### RabbitMQ
Broker de mensajería para comunicación entre microservicios.

| Configuración | Valor |
|---------------|-------|
| **Imagen** | `rabbitmq:3-management` |
| **Container** | `microservices-rabbitmq` |
| **Puerto AMQP** | `5672:5672` |
| **Puerto Management UI** | `15672:15672` |
| **Usuario** | `admin` |
| **Contraseña** | `admin123` |

### SQL Server
Base de datos relacional Microsoft SQL Server.

| Configuración | Valor |
|---------------|-------|
| **Imagen** | `mcr.microsoft.com/mssql/server:2019-latest` |
| **Container** | `microservices-sqlserver` |
| **Puerto** | `1434:1433` |
| **Usuario SA Password** | `Password123!` |
| **Edición** | Developer |

### Redis
Cache en memoria para almacenamiento de datos de alta velocidad.

| Configuración | Valor |
|---------------|-------|
| **Imagen** | `redis:7-alpine` |
| **Container** | `microservices-redis` |
| **Puerto** | `6379:6379` |

## Uso

### Iniciar todos los servicios
```bash
docker-compose up -d
```

### Detener todos los servicios
```bash
docker-compose down
```

### Ver logs de los servicios
```bash
docker-compose logs -f
```

### Ver estado de los servicios
```bash
docker-compose ps
```

## Acceso a las interfaces de administración

| Servicio | URL |
|----------|-----|
| **RabbitMQ Management** | http://localhost:15672 |
| **LocalStack** | http://localhost:4566 |

## Volúmenes persistentes

Los siguientes volúmenes se crean para persistir datos entre reinicios:

- `sqlserver-data`: Datos de SQL Server
- `rabbitmq-data`: Datos de RabbitMQ
- `redis-data`: Datos de Redis
- `localstack-data`: Datos de LocalStack

## Red

Todos los servicios están conectados a la red `microservices-network` con driver bridge, permitiendo la comunicación entre contenedores.
