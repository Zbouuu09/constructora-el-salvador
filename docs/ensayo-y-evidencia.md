# T0.6 · Prueba cruzada y ensayo de proyección

Este archivo es un guion y una plantilla de registro. No acredita que el equipo se haya reunido ni que otro compañero haya probado la aplicación. La fecha del plan original es 2026-09-25, “Viernes 25 en Sesión 15”; anotar la fecha real de ejecución a continuación.

## Guion de prueba real

Usar la URL pública desplegada, datos de cliente ficticios y un navegador de otro equipo o conexión. La persona que verifica debe ser distinta del autor del componente probado.

| Paso | Acción | Resultado esperado | Resultado observado / evidencia |
| --- | --- | --- | --- |
| 1 | Abrir URL pública y health. | Sitio y API disponibles; sin depender de `localhost`. | Pendiente. |
| 2 | Cargar catálogo en la UI y abrir `GET /api/maquinaria`. | CAT 336 y JCB 3CX obtenidas de la API. | Pendiente. |
| 3 | Elegir máquina, cliente «Cliente demo» y un periodo válido. | Se muestra selección y total conforme a tarifa diaria y días inclusivos. | Pendiente. |
| 4 | Enviar formulario. | Respuesta HTTP `201`; confirmación con ID UUID y total. | Pendiente. |
| 5 | Consultar `GET /api/contratos/<ID devuelto>` desde otro navegador. | El mismo contrato está guardado en PostgreSQL. | Pendiente. |
| 6 | Crear contrato de un único día. | Un día de alquiler, sin total cero. | Pendiente. |
| 7 | Probar cliente vacío, máquina inexistente, fecha inválida y fin anterior al inicio por API. | Respuestas de error claras; ningún contrato inválido guardado. | Pendiente. |
| 8 | Enviar reserva superpuesta si la aplicación valida disponibilidad. | Rechazo controlado; sin duplicar una reserva incompatible. | Pendiente; registrar si forma parte de la implementación. |
| 9 | Revisar el PR y sus checks en GitHub. | `Pruebas` pasa, revisión auténtica y conversaciones resueltas. | Pendiente. |
| 10 | Integrar por PR y esperar despliegue desde `main`. | URL muestra la versión integrada; anotar commit y despliegue. | Pendiente. |

Para la evidencia de API, guardar el método, ruta, cuerpo de solicitud de prueba, código HTTP y respuesta. Ocultar credenciales, cadenas de conexión y datos personales. Ante un fallo, registrar el resultado real y repetir sólo después de corregirlo.

## Ensayo con proyector · 5 minutos

1. **Preparación, antes de iniciar:** conectar el equipo que se utilizará, verificar red, abrir la URL pública y esperar la reactivación de Render si estaba suspendido. Ajustar zoom para que catálogo, fechas y confirmación sean legibles desde el aula.
2. **0:00–0:45:** presentar el objetivo: alquilar maquinaria y registrar un contrato real en la base compartida. Mostrar la URL pública.
3. **0:45–2:00:** consultar catálogo, elegir CAT 336 o JCB 3CX y completar cliente ficticio y fechas válidas. Explicar el periodo y total.
4. **2:00–3:00:** crear contrato, mostrar confirmación y leer el ID. Recuperarlo por API para demostrar persistencia.
5. **3:00–4:00:** mostrar un caso inválido y su mensaje; mostrar brevemente el PR revisado y `Pruebas`.
6. **4:00–5:00:** el compañero ejecuta el recorrido desde su equipo. Mostrar resultado y los puntos completados de la Definition of Done.

Si la nube falla, registrar el fallo y usar la copia local para explicar el flujo mientras se corrige. La demostración local no cierra el requisito de URL pública ni sustituye la prueba exterior.

## Ficha de evidencia

| Campo | Valor |
| --- | --- |
| Fecha y hora real, zona El Salvador | Pendiente. |
| URL pública comprobada | Pendiente. |
| Commit y enlace de despliegue | Pendiente. |
| Componente probado y su autor | Pendiente. |
| Compañero que hizo la prueba | Pendiente. |
| Equipo/navegador y conexión utilizada | Pendiente. |
| ID del contrato de prueba | Pendiente. |
| Respuesta de consulta del contrato | Pendiente. |
| Enlace del PR y revisión | Pendiente. |
| Enlace del check `Pruebas` | Pendiente. |
| Capturas o registro de API sin secretos | Pendiente. |
| Resultado del ensayo con proyector | Pendiente. |
| Fallos encontrados, corrección y repetición | Pendiente. |
| Resultado final | Pendiente: aprobado / falló / bloqueado, según evidencia. |

Tras la ejecución, sustituir «Pendiente» por hechos observados y actualizar [seguimiento](seguimiento-sprint.md). No rellenar nombres, aprobaciones, reuniones ni resultados por anticipado.
