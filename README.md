# Constructora El Salvador · Sprint 0

Base funcional para consultar maquinaria y registrar contratos de alquiler. La interfaz y la API se sirven desde el mismo sitio; PostgreSQL conserva los datos en la nube y PGlite permite trabajar localmente.

## Iniciar en Windows

Requisitos: Node.js 24 y npm. Abre una terminal en esta carpeta y ejecuta:

```powershell
npm ci
npm start
```

Abre [http://localhost:3000](http://localhost:3000). Para el modo local deja `DATABASE_URL` sin configurar. Para usar PostgreSQL, configura esa variable en un `.env` privado siguiendo `.env.example`.

```powershell
npm test
npm run db:init
npm run db:seed
```

Los dos últimos comandos preparan las tablas y el catálogo. Ejecuta los comandos con la misma configuración de base de datos que utilizará la aplicación.

## Flujo de demostración

1. Consultar el catálogo de CAT 336 y JCB 3CX.
2. Elegir maquinaria y escribir cliente, fecha inicial y fecha final.
3. Crear el contrato y conservar el ID de confirmación. El total incluye ambos días del periodo.
4. Consultar el contrato guardado con `GET /api/contratos/:id`.

| API | Resultado esperado |
| --- | --- |
| `GET /api/maquinaria` | Lista de maquinaria en JSON. |
| `POST /api/contratos` | Guarda un contrato válido; responde `201` con ID UUID y total. |
| `GET /api/contratos/:id` | Consulta el contrato por su ID. |

El cuerpo del POST usa `maquinaria_id`, `cliente`, `fecha_inicio` y `fecha_fin`. Usa un ID obtenido del catálogo y fechas `AAAA-MM-DD`.

## Entrega del sprint

- [Tareas, responsables y estado](docs/seguimiento-sprint.md).
- [Repositorio, ramas y publicación en Render](docs/despliegue.md).
- [Prueba cruzada y ensayo con proyector](docs/ensayo-y-evidencia.md).

El repositorio previsto es `Zbouuu09/constructora-el-salvador`. La guía de publicación no demuestra que el repositorio remoto o los servicios ya existan: la evidencia de cada paso se registra en el seguimiento. Nunca subas `.env`, contraseñas ni cadenas de conexión a GitHub o a la hoja compartida.
