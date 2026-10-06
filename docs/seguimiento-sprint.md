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

La API, la interfaz y el modelo están implementados. Las 13 pruebas automáticas aprobaron contra PostgreSQL embebido PGlite, y el catálogo, la creación y la consulta de contratos se comprobaron en PostgreSQL de Render. También aprobó una prueba de integración DOM con la API local. El recorrido del formulario público y su revisión visual aprobaron en un navegador real automatizado; el contrato se recuperó después por una consulta HTTP independiente. La prueba cruzada de un compañero y el ensayo del equipo con proyector siguen pendientes.

| Área | Estado a registrar | Evidencia |
| --- | --- | --- |
| Implementación local de API, UI y modelo | Implementada; 13/13 pruebas backend e integración DOM + API aprobadas. | [Resultados](resultados-pruebas.md). |
| Recorrido del formulario público y revisión visual | Aprobados con navegador real automatizado: catálogo de dos máquinas, JCB 3CX, 2026-10-23 a 2026-10-25, 3 días y USD 825; confirmación y consulta independiente HTTP 200. | [Evidencia de navegador](evidencia-navegador.json); contrato `de5a887a-fa57-4b23-8306-325153056f23`; captura entregada `contrato-publico.jpg`. El ensayo con proyector sigue pendiente. |
| Repositorio remoto y ramas | Código del PR #1 integrado en `main`; verificadas `ivan`, `kevin`, `jose`, `mariela`, `victor`. El acceso real de los compañeros sigue pendiente de acreditación. | [Repositorio](https://github.com/Zbouuu09/constructora-el-salvador), [PR #1 integrado](https://github.com/Zbouuu09/constructora-el-salvador/pull/1). |
| Protección de `main` | Ruleset activo y verificado sobre la rama predeterminada; bloquea borrado y force push. Exige el check `Pruebas` de GitHub Actions, PR con una aprobación y conversaciones resueltas. | [Regla](https://github.com/Zbouuu09/constructora-el-salvador/settings/rules/24590775); API confirmó `active`, `~DEFAULT_BRANCH`, `integration_id: 15368`, `required_approving_review_count: 1` y `required_review_thread_resolution: true`. |
| PostgreSQL compartido | Instancia gratuita activa; catálogo y contrato guardado comprobados por la API pública. Compartir la conexión privada al equipo sigue pendiente. | Recurso `dpg-db2h0mmi0phs73elivo0-a`, PostgreSQL 17; health informa `postgresql`; contrato `1cc18688-2405-48e3-93a6-20ab9678fe28`. |
| CI de GitHub | Ejecución del PR #1 aprobada (`success`). | [CI del PR #1](https://github.com/Zbouuu09/constructora-el-salvador/actions/runs/37486556228). |
| Sitio público y despliegue automático | Despliegue `live` verificado; conectado a `main` con `autoDeployTrigger: checksPass`. | [Aplicación](https://constructora-el-salvador.onrender.com), despliegue `dep-db2h560m7kps73erjmi0`, commit `69040e72f10ace91b61933001828132ccdfff8d1`. |
| Revisión de PR por otro integrante | PR #1 integrado tras revisión técnica automatizada. PR #2 abierto para revisión y aprobación humanas; no se acredita una aprobación de otro integrante. | [PR #1 integrado](https://github.com/Zbouuu09/constructora-el-salvador/pull/1), [PR #2 pendiente de aprobación humana](https://github.com/Zbouuu09/constructora-el-salvador/pull/2), [resultados](resultados-pruebas.md). |
| Prueba cruzada y ensayo con proyector | Pendiente de realización por el equipo. | Pendiente: ficha de [ensayo y evidencia](ensayo-y-evidencia.md). |

## Definition of Done

- [ ] Repositorio remoto accesible a los integrantes del equipo; las cinco ramas y la protección de `main` están verificadas, pero falta acreditar el acceso de los compañeros.
- [x] La comprobación `Pruebas` de GitHub pasa para la versión integrada mediante el PR #1.
- [x] Render publica la versión integrada desde `main`; URL y health funcionan desde fuera del equipo de desarrollo.
- [x] PostgreSQL contiene CAT 336 y JCB 3CX; un contrato creado mediante la API puede consultarse por su ID.
- [x] El formulario del sitio público completa el recorrido catálogo → selección → contrato → confirmación; el contrato se recuperó por ID después de la prueba en navegador real.
- [x] Cliente vacío, maquinaria inexistente, fechas inválidas y fecha final anterior a la inicial se rechazan sin guardar contratos inválidos.
- [ ] Un compañero distinto del autor ejecuta el recorrido y deja evidencia auténtica.
- [ ] El PR #2 tiene la aprobación humana requerida y sus conversaciones están resueltas antes del merge.
- [ ] El equipo ensaya en el equipo/proyector que usará y registra el resultado.
- [ ] La hoja registra evidencia o estado pendiente; no contiene secretos ni resultados inventados.
