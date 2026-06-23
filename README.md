# Sistema de Gestión de Bibliotecas Digitales
**Evaluación EP3 - Desarrollo FullStack I (DSY1103) - DuocUC**

## Integrantes
- Cristóbal Gonzalez
- Javier Cataldo
- Vicente Barrera

## Descripción
Sistema de microservicios para la gestión de una biblioteca digital, desarrollado con Spring Boot 3.5.14 y Spring Cloud 2025.0.3.

## Microservicios
| Servicio | Puerto | Descripción |
|---|---|---|
| msAutores | 8081 | Gestión de autores |
| msCategoria | 8082 | Gestión de categorías |
| msEditoriales | 8083 | Gestión de editoriales |
| msEjemplares | 8084 | Gestión de ejemplares |
| msLibros | 8085 | Gestión de libros (consume msAutores, msCategoria, msEditoriales) |
| msGateway | 8080 | API Gateway - punto único de entrada |

## Tecnologías
- Java 17
- Spring Boot 3.5.14
- Spring Cloud Gateway 2025.0.3
- MySQL (Laragon local / Railway remoto)
- Docker
- JUnit 5 + Mockito (46 pruebas unitarias)
- JaCoCo (cobertura de código)
- Swagger/OpenAPI (springdoc 2.8.5)

## Ejecución Local
### Requisitos
- Java 17
- Maven
- MySQL (Laragon)
- Docker Desktop

### Con Maven
```bash
cd msAutores/msAutores && ./mvnw spring-boot:run
cd msCategoria/msCategoria && ./mvnw spring-boot:run
cd msEditoriales/msEditoriales && ./mvnw spring-boot:run
cd msEjemplares/msEjemplares && ./mvnw spring-boot:run
cd msLibros/msLibros && ./mvnw spring-boot:run
cd msGateway/msGateway && ./mvnw spring-boot:run
```

### Con Docker
```bash
docker run -d --name ms-autores -p 8081:8081 -e SPRING_PROFILES_ACTIVE=dev -e SPRING_DATASOURCE_URL="jdbc:mysql://host.docker.internal:3306/gestion_biblioteca" ms-autores:latest
docker run -d --name ms-categorias -p 8082:8082 -e SPRING_PROFILES_ACTIVE=dev -e SPRING_DATASOURCE_URL="jdbc:mysql://host.docker.internal:3306/gestion_biblioteca" ms-categorias:latest
docker run -d --name ms-editoriales -p 8083:8083 -e SPRING_PROFILES_ACTIVE=dev -e SPRING_DATASOURCE_URL="jdbc:mysql://host.docker.internal:3306/gestion_biblioteca" ms-editoriales:latest
docker run -d --name ms-ejemplares -p 8084:8084 -e SPRING_PROFILES_ACTIVE=dev -e SPRING_DATASOURCE_URL="jdbc:mysql://host.docker.internal:3306/gestion_biblioteca" ms-ejemplares:latest
docker run -d --name ms-libros -p 8085:8085 -e SPRING_PROFILES_ACTIVE=dev -e SPRING_DATASOURCE_URL="jdbc:mysql://host.docker.internal:3306/gestion_biblioteca" ms-libros:latest
```

## Rutas del Gateway (puerto 8080)
| Ruta | Microservicio destino |
|---|---|
| /api/autores/** | msAutores:8081 |
| /api/categorias/** | msCategoria:8082 |
| /api/editoriales/** | msEditoriales:8083 |
| /api/ejemplares/** | msEjemplares:8084 |
| /api/libros/** | msLibros:8085 |

## Swagger UI
- msAutores: http://localhost:8081/swagger-ui/index.html
- msCategoria: http://localhost:8082/swagger-ui/index.html
- msEditoriales: http://localhost:8083/swagger-ui/index.html
- msEjemplares: http://localhost:8084/swagger-ui/index.html
- msLibros: http://localhost:8085/swagger-ui/index.html
