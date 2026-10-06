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

## Integración de la interfaz con la API local

Una prueba DOM con JSDOM ejecutó el JavaScript entregado contra la API local: cargó las dos tarjetas, seleccionó CAT 336 y calculó 3 días / USD 1,350 para 2055-10-20 a 2055-10-22. El botón de envío produjo exactamente un POST con HTTP 201; la confirmación mostró el ID `8f4db162-ed72-4248-aaac-ddbba4ad9c21`. La consulta posterior del ID devolvió el contrato esperado.

Al iniciar otro contrato con fechas invertidas, la interfaz mostró el error, enfocó la fecha final y no envió otro POST. No se registraron errores de JSDOM. Esta verificación acredita la lógica DOM y su conexión con la API. La prueba posterior en el navegador público se registra a continuación.

## Verificación de PostgreSQL administrado

El despliegue `dep-db2h560m7kps73erjmi0` de Render está `live`, sin errores de aplicación en la consulta de logs realizada. [La aplicación pública](https://constructora-el-salvador.onrender.com) ejecuta el commit integrado `69040e72f10ace91b61933001828132ccdfff8d1`; su publicación automática está vinculada a `main` y espera las comprobaciones de CI.

| Comprobación en la URL pública | Resultado |
| --- | --- |
| `GET /api/health` | HTTP 200; `database: postgresql`. |
| `GET /api/maquinaria` | HTTP 200; CAT 336 y JCB 3CX. |
| POST CAT 336, 2026-10-20 a 2026-10-22 | HTTP 201; 3 días; USD 1,350. |
| ID generado en nube | `1cc18688-2405-48e3-93a6-20ab9678fe28`. |
| GET del contrato generado | HTTP 200; objeto idéntico al creado. |
| Repetir el intervalo reservado | HTTP 409, `DATE_CONFLICT`. |
| Fin anterior al inicio | HTTP 400. |

El cliente usado es de demostración. La base sólo admite conexiones de red privadas; la comprobación anterior se realizó a través de la API de la aplicación, sin abrir el acceso externo a PostgreSQL.

Render informa que esta instancia del plan gratuito vence el **5 de noviembre de 2026**. Su identificador es `dpg-db2h0mmi0phs73elivo0-a`; conviene exportar los datos o decidir una continuidad antes de esa fecha.

## Recorrido y revisión visual en navegador público

El 6 de octubre de 2026 se completó el recorrido de [la aplicación pública](https://constructora-el-salvador.onrender.com) con un navegador real automatizado. Render mostró su arranque tras inactividad antes de cargar; después el sitio quedó funcional. El catálogo presentó CAT 336 y JCB 3CX. Se seleccionó JCB 3CX, se completó el cliente ficticio «Demostración navegador Sprint 0» y el periodo 2026-10-23 a 2026-10-25; la interfaz mostró 3 días y USD 825.

El formulario generó la confirmación `de5a887a-fa57-4b23-8306-325153056f23`. Una consulta HTTP independiente a `GET /api/contratos/de5a887a-fa57-4b23-8306-325153056f23` respondió `200` y confirmó maquinaria, cliente, fechas, duración, tarifa diaria de USD 275, total de USD 825 y estado `CONFIRMADO` guardados en PostgreSQL. La revisión visual aprobó y la consola del navegador no registró errores ni advertencias.

El registro está en [evidencia de navegador](evidencia-navegador.json) y la captura `contrato-publico.jpg` se incluye en la entrega. Esta comprobación automatizada acredita el recorrido en navegador real; la prueba cruzada de un compañero y la legibilidad en el equipo/proyector del aula siguen pendientes.

## Pendiente

- Revisar la legibilidad y ensayar con el equipo/proyector real.
- Comprobar el despliegue automático después de una actualización aprobada de `main`.
- Registrar la prueba cruzada de un integrante real y su evidencia.
- Obtener la revisión y aprobación humanas del [PR #2 abierto](https://github.com/Zbouuu09/constructora-el-salvador/pull/2) antes de integrarlo.
- Acreditar el acceso de los compañeros al repositorio y compartir la conexión de PostgreSQL por un canal privado.

Las comprobaciones HTTP, DOM y de navegador automatizado no se atribuyen a los integrantes del equipo ni se presentan como un ensayo con proyector realizado.
