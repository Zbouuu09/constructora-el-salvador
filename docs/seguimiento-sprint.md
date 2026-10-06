# Seguimiento de Sprint 0

Fuente: [hoja del sprint](https://docs.google.com/spreadsheets/d/118feVEbHNlqrD7DXdDwxM1A-rCo7-j807eX0JDnZCK4/edit). Las fechas y los responsables de esta tabla se conservan tal como aparecen en el plan original. Son fechas de septiembre de 2026; no se presentan como un calendario futuro.

| Tarea | Responsable original | Fecha original | Estado original | Entregable y criterio de cierre |
| --- | --- | --- | --- | --- |
| T0.1 · Repositorio base y cinco ramas | Iván Vásquez | 2026-09-23 | IN PROGRESS | Repositorio remoto accesible, base Frontend/Backend, ramas `ivan`, `kevin`, `jose`, `mariela`, `victor` y protección efectiva de `main`. |
| T0.2 · Infraestructura y despliegue CI/CD | Kevin Landos | 2026-09-23 | IN PROGRESS | Render conectado al repositorio, publicación automática desde `main` y URL pública comprobada desde otro equipo o conexión. Es la “Meta no negociable para el proyector”. |
| T0.3 · Base de datos compartida y modelo mínimo | José Sandoval | 2026-09-24 | TODO | PostgreSQL en la nube con tablas de maquinaria y contratos/reservas, CAT 336 y JCB 3CX en el catálogo, conexión disponible privadamente al equipo. Depende de T0.1. |
| T0.4 · Endpoints mínimos de API | Mariela Flores | 2026-09-24 | TODO | `GET /api/maquinaria` y `POST /api/contratos` consultan/escriben en la base real; evidencia de prueba por Postman o URL. Depende de T0.3. |
| T0.5 · Interfaz y conexión extremo a extremo | Víctor Quijada | 2026-09-25 | TODO | Catálogo obtenido por GET, formulario de maquinaria/cliente/fechas, POST y confirmación con ID. Depende de T0.4. |
| T0.6 · Verificación cruzada, DoD y ensayo | Todo el equipo | 2026-09-25 | TODO | Flujo completo en la URL pública, prueba por un compañero ajeno al código probado, revisión de PR y merge en `main`, ensayo de proyección. Referencia original: “Viernes 25 en Sesión 15”. |

## Ejecución por responsable

1. **Iván:** publicar la base en el repositorio autorizado, crear las cinco ramas, incorporar a los colaboradores reales y aplicar la protección de `main` descrita en [despliegue](despliegue.md). Guardar enlace del repositorio y captura de ramas/protección.
2. **Kevin:** conectar GitHub con Render, aplicar `render.yaml`, esperar un despliegue saludable y comprobar el sitio desde una conexión exterior. Registrar URL y enlace al despliegue; comprobar una actualización posterior de `main` aprobada por PR.
3. **José:** ejecutar inicialización y seed sobre PostgreSQL, verificar las dos máquinas y registrar el nombre del recurso y los resultados sin mostrar credenciales. Compartir `DATABASE_URL` únicamente por un canal privado del equipo.
4. **Mariela:** ejecutar GET, POST válido y casos inválidos contra la URL pública; recuperar el contrato por ID para demostrar persistencia. Anotar solicitudes, códigos HTTP y respuestas sin datos personales reales.
5. **Víctor:** probar en el navegador el catálogo y el formulario conectado a la API; revisar confirmación, validación y legibilidad para proyección. Conservar captura de la confirmación y del ID.
6. **Todo el equipo:** ejecutar [el guion de verificación](ensayo-y-evidencia.md), completar la prueba cruzada y revisar el PR antes del merge. Registrar a las personas que realmente participaron y sus resultados.

## Estado de la entrega y evidencia

La API, la interfaz y el modelo están implementados. Las 13 pruebas automáticas aprobaron contra PostgreSQL embebido PGlite, incluida la reapertura de la base, rollback y reservas simultáneas. La verificación de navegador y de la nube permanece separada: no se marca una tarea `DONE` únicamente por disponer de archivos locales.

| Área | Estado a registrar | Evidencia |
| --- | --- | --- |
| Implementación local de API, UI y modelo | Implementada; 13/13 pruebas automáticas aprobadas. | Node 24.19.0: `node --test --test-isolation=none backend/*.test.mjs`. Prueba de navegador pendiente. |
| Repositorio remoto y ramas | Código integrado en `main`; verificadas `ivan`, `kevin`, `jose`, `mariela`, `victor`. | [Repositorio](https://github.com/Zbouuu09/constructora-el-salvador), [PR #1 integrado](https://github.com/Zbouuu09/constructora-el-salvador/pull/1). |
| Protección de `main` | Pendiente de aplicación/verificación. | Pendiente: captura o configuración comprobada. |
| PostgreSQL compartido | Instancia gratuita creada en Render, estado `available`; tablas y contratos en nube pendientes. | Recurso `dpg-db2h0mmi0phs73elivo0-a`, región Oregon, PostgreSQL 17. |
| CI de GitHub | Ejecución de PR aprobada (`success`). | [CI del PR #1](https://github.com/Zbouuu09/constructora-el-salvador/actions/runs/37486556228). |
| Sitio público y despliegue automático | Pendiente de despliegue/verificación. | Pendiente: URL, health y actualización desde `main`. |
| Revisión de PR por otro integrante | Revisión técnica automatizada e integración realizadas; aprobación humana pendiente. | [PR #1](https://github.com/Zbouuu09/constructora-el-salvador/pull/1), [resultados](resultados-pruebas.md). |
| Prueba cruzada y ensayo con proyector | Pendiente de realización por el equipo. | Pendiente: ficha de [ensayo y evidencia](ensayo-y-evidencia.md). |

## Definition of Done

- [ ] Repositorio remoto accesible al equipo con las cinco ramas y `main` protegida.
- [ ] La comprobación `Pruebas` de GitHub pasa para el cambio que se presenta.
- [ ] Render publica la versión integrada desde `main`; URL y health funcionan desde fuera del equipo de desarrollo.
- [ ] PostgreSQL contiene CAT 336 y JCB 3CX; un contrato creado mediante la API puede consultarse por su ID.
- [ ] El formulario del sitio público completa el recorrido catálogo → selección → contrato → confirmación.
- [ ] Cliente vacío, maquinaria inexistente, fechas inválidas y fecha final anterior a la inicial se rechazan sin guardar contratos inválidos.
- [ ] Un compañero distinto del autor ejecuta el recorrido y deja evidencia auténtica.
- [ ] El PR tiene la revisión requerida y sus conversaciones están resueltas antes del merge.
- [ ] El equipo ensaya en el equipo/proyector que usará y registra el resultado.
- [ ] La hoja registra evidencia o estado pendiente; no contiene secretos ni resultados inventados.
