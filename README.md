# Pagos — Microservicio de riesgo pagos

Microservicio correspondiente al **caso casoEjemplo — TicketWave** (Venta y control de acceso de entradas para eventos en vivo) de la Evaluación Parcial N°1.

| | |
|---|---|
| Stack | Spring Boot 3.3 · Java 21 · Maven · Spring Data JPA · H2 · springdoc-openapi |
| Calidad | JaCoCo cobertura LINE 100% · Cucumber (BDD) alineado a endpoints REST |
| Entrega | Docker / Docker Compose |

## Responsabilidad (SRP)

administra los datos y la lógica del dominio de Pagos del caso casoEjemplo (TicketWave). Su base de datos es una **H2 en memoria** (un solo microservicio por base), cumpliendo aislamiento de datos por dominio.

## Página de presentación

Al ejecutar el servicio, `http://localhost:8080/` muestra la página de presentación del microservicio con documentación y enlaces a:

- **Swagger UI**: `/swagger-ui/index.html`
- **OpenAPI (yaml)**: `/v3/api-docs.yaml`
- **ReDoc**: `/redoc.html`
- **H2 Console**: `/h2-console`

## Endpoints

| Método | Ruta | Descripción |
|--------|------|-------------|
| GET | `/api/pagos` | Lista todos los recursos |
| GET | `/api/pagos/{id}` | Obtiene un recurso por id |
| POST | `/api/pagos` | Crea un recurso |
| PUT | `/api/pagos/{id}` | Actualiza un recurso |
| DELETE | `/api/pagos/{id}` | Elimina un recurso |

## Documentación del proyecto

La documentación completa está en la carpeta [`docs/`](docs/):

- [`docs/00_Resumen.md`](docs/00_Resumen.md) — propósito, responsabilidad y tecnologías
- [`docs/01_Arquitectura.md`](docs/01_Arquitectura.md) — componentes, arquitectura y patrones
- [`docs/02_API.md`](docs/02_API.md) — contrato REST y ejemplos curl
- [`docs/03_Pruebas.md`](docs/03_Pruebas.md) — tests unitarios, cobertura y Cucumber
- [`docs/04_Despliegue.md`](docs/04_Despliegue.md) — Docker, Docker Compose e integración

## Cómo ejecutar locmente

```bash
mvn spring-boot:run
```

## Cómo ejecutar con Docker

```bash
docker compose up --build
# http://localhost:8080
```

## Cómo ejecutar las pruebas

```bash
mvn test      # unit tests + Cucumber
mvn verify    # + verificación de cobertura JaCoCo (100% LINE, falla si baja)
```

## Modelo de ramificacion elegido: Gitflow

- Usamos este modelo porque es el mas adecuado para el proyecto, se encarga de separar el codigo en desarrollo del codigo estable,  permite subir nuevas funciones sin ensuciar el codigo principal y
  facilita la correcion inmediata de fallos criticos.

  ## Convenciones y buenas prácticas del equipo

### 1. Convención de commits
Seguimos el formato estándar: `tipo(alcance): descripcion-corta` (en minúsculas y sin tildes).

| Tipo | Propósito | Ejemplo |
| :--- | :--- | :--- |
| `feat` | Nueva funcionalidad | `feat(ui): agregar pie de pagina` |
| `fix` | Corrección de bug | `fix(home): corregir titulo` |
| `docs` | Documentación | `docs: agregar changelog` |
| `chore` | Tareas de mantenimiento o CI/CD | `chore(ci): agregar workflow hola mundo` |

### 2. Naming de ramas
* Formato: `feature/<nombre>` y `hotfix/<nombre>`[cite: 1].
* Todo en minúsculas y con palabras separadas por guiones[cite: 1].
* Ejemplos: `feature/pagina-presentacion`, `hotfix/titulo-pagina`[cite: 1].

### 3. Flujo de merge
* Las ramas `feature/` y `hotfix/` siempre ingresan mediante Pull Request; nunca se realiza `push` directo a `main` ni a `develop`[cite: 1].
* Se exige al menos una aprobación obligatoria del compañero antes de realizar el merge[cite: 1].
* Se utiliza *merge commit* o *squash*, y la rama remota debe borrarse tras la integración[cite: 1].

### 4. Estrategia de revisión
* El autor abre el PR, completa la descripción y asigna formalmente a su compañero como revisor[cite: 1].
* El revisor examina la pestaña de cambios (*diff*), deja comentarios si es necesario y aprueba (*Approve*) antes de fusionar[cite: 1].
* Antes de solicitar revisión, se debe comprobar localmente que las pruebas del proyecto se ejecutan de manera satisfactoria[cite: 1].
