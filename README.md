# FLY API — Backend Modular

> **Repositorio principal del backend para la plataforma FLY Data Platform.**
>
> Aquí se desarrollan todos los dominios funcionales y técnicos bajo una arquitectura modular por dominio (by module), siguiendo buenas prácticas de desacoplamiento, escalabilidad y mantenibilidad.

---

## 🚀 ¿Qué contiene este repositorio?

Este repositorio implementa el backend de la plataforma FLY, alineado con el baseline arquitectónico y de datos validado en PostgreSQL 16. Aquí se encuentran:

- **Servicios API** sobre todos los dominios de negocio y operación.
- **Arquitectura modular**: cada dominio es un módulo independiente, facilitando la evolución y el testing.
- **Integración con base de datos**: este backend consume la base de datos `fly_db`, pero **NO mantiene scripts de migraciones ni seeds**; toda la gestión de migraciones, datos de inicio y parametrizaciones iniciales se delega al repositorio [fly-db](https://github.com/code-corhuila/fly-db).
- **Controles de calidad y CI/CD**: flujos de integración continua, validaciones automáticas y promoción controlada.
- **Evidencias y artefactos**: enlaces a scripts, seeds, migraciones y reportes funcionales.

---

## 🏗️ Arquitectura y dominios

El backend está organizado por módulos, cada uno representando un dominio funcional:

| Dominio              | Tablas principales                        |
|----------------------|-------------------------------------------|
| Identidad            | person, documents, contacts, user_account |
| Cliente              | customer, category, benefits, loyalty     |
| Red aeroportuaria    | country, city, airport, terminal, gate    |
| Operación aérea      | airline, aircraft, flight, segment        |
| Comercial            | reservation, sale, ticket, seat assignment|
| Recaudo              | payment, transaction, invoice, refund     |

Cada módulo expone servicios REST y lógica de negocio desacoplada.

---

## 🔗 Artefactos y recursos clave

- **Modelo de datos**: mantenido en [fly-db](https://github.com/code-corhuila/fly-db)
- **Migraciones y seeds**: mantenidos en [fly-db](https://github.com/code-corhuila/fly-db)
- **Scripts de operación**: mantenidos en [fly-db](https://github.com/code-corhuila/fly-db)
- **Evidencias de CI/CD**: docs/validacion/EVIDENCIA_PIPELINE_CI_REMOTO_2026-03-20.md
- **Canvas arquitectónico**: architecture/canvas/canvas_arquitectura.html

---

## 🛠️ Stack tecnológico

- **Java 17** (Spring Boot 3+)
- **PostgreSQL 16**
- **Maven**
- **CI/CD**: GitHub Actions
- **Hibernate**: modo `create-drop` para desarrollo (la base se crea y elimina automáticamente, pero los datos y estructura reales provienen de [fly-db](https://github.com/code-corhuila/fly-db))

---

## 📦 Estructura modular (by module)

Cada dominio se implementa como un módulo independiente, siguiendo patrones DDD y separación de capas:

- `api-<dominio>`: Controladores, servicios y lógica de negocio de cada dominio.
- `core`: Utilidades y componentes compartidos.
- `infra`: Integraciones, scripts y herramientas de operación.

---

## 📝 ¿Cómo empezar?

1. Clona el repositorio y asegúrate de tener la base de datos `fly_db` ya creada y poblada usando los scripts y migraciones del repo [fly-db](https://github.com/code-corhuila/fly-db).
2. Configura Hibernate en modo `validate` solo para desarrollo local.
3. Desarrolla o extiende módulos según el dominio requerido.
4. Usa los scripts y flujos de CI para validar cambios antes de promoverlos.

---

## 📚 Referencias y documentación

- [fly-db — Migraciones y modelo de datos](https://github.com/code-corhuila/fly-db)
- Canvas de arquitectura
- Informe funcional
- Roadmap de estabilización
- Evidencias de validación

---

## 🏷️ Generado con Spring Initializr

https://start.spring.io/#!type=maven-project&language=java&platformVersion=4.0.5&packaging=jar&configurationFileFormat=properties&jvmVersion=17&groupId=com.fly-api&artifactId=api&packageName=com.fly-api.api&dependencies=web,postgresql,devtools,data-jpa