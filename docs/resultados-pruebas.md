# Resultados de pruebas

Verificación del 6 de octubre de 2026. Las comprobaciones locales y remotas se distinguen de las actividades pendientes del equipo.

## Pruebas automáticas

13 de 13 pruebas aprobadas, sin fallos ni omisiones, en Node.js 24.19.0 con PostgreSQL embebido PGlite. Cubren catálogo, creación y consulta por ID, consulta SQL independiente, validación, calendario, límites HTTP, maquinaria no disponible, solapamientos inclusivos, solicitudes simultáneas, rollback, reapertura persistente y exigencia de PostgreSQL remoto en producción.

En este entorno local se ejecutó `node --test --test-isolation=none backend/*.test.mjs`; la opción evita el aislamiento por subprocesos restringido por el entorno. GitHub ejecutó el comando normal `npm test` y aprobó [la comprobación del PR #1](https://github.com/Zbouuu09/constructora-el-salvador/actions/runs/37486556228).

## Verificación HTTP independiente local

| Comprobación | Resultado observado |
| --- | --- |
| Health y catálogo | HTTP 200; CAT 336 y JCB 3CX con tarifas numéricas. |
| HTML, JavaScript, CSS y favicon | HTTP 200 y tipo de contenido correcto. |
| Crear contrato CAT 336, 2050-11-14 a 2050-11-16 | HTTP 201; 3 días; USD 1,350. |
| ID generado | `19721f14-ec08-407c-93aa-36772fe18340`. |
| Consultar el contrato por ID | HTTP 200; contenido idéntico al creado. |
| Repetir fechas superpuestas | HTTP 409, `DATE_CONFLICT`. |
| Calendario imposible, fin anterior o cliente vacío | HTTP 400. |
| Maquinaria inexistente | HTTP 404. |

La revisión independiente del código no encontró defectos que bloqueen este recorrido. Se verificaron parámetros SQL, cálculo del total en el servidor y transacción con bloqueo y rollback.

## Pendiente

- Ejecutar el recorrido en el navegador y en la URL pública con PostgreSQL administrado.
- Comprobar el despliegue automático después de una actualización aprobada de `main`.
- Registrar la prueba cruzada de un integrante real, su aprobación de PR y el ensayo con el proyector.

Estas comprobaciones HTTP y la revisión automatizada no se atribuyen a los integrantes del equipo ni se presentan como un ensayo realizado.
