# Repositorio, CI y despliegue

El repositorio [Zbouuu09/constructora-el-salvador](https://github.com/Zbouuu09/constructora-el-salvador) y [la aplicación pública](https://constructora-el-salvador.onrender.com) están publicados con Node.js y PostgreSQL en Render. Esta guía permite reproducir la configuración; los resultados y pendientes están en [seguimiento](seguimiento-sprint.md).

## T0.1 · Repositorio y ramas

El propietario crea el repositorio en GitHub, carga los archivos del proyecto y añade a los colaboradores por sus usuarios reales. No se deben adivinar los usuarios de los integrantes. Después del primer commit de `main`, los comandos para crear las ramas son:

```powershell
git fetch origin
git switch main
git pull --ff-only origin main
git branch ivan
git branch kevin
git branch jose
git branch mariela
git branch victor
git push origin ivan kevin jose mariela victor
```

Si una rama ya existe, úsala; no la elimines ni la reemplaces. Cada integrante trabaja en su rama, incorpora sólo sus cambios y abre un Pull Request hacia `main` con el número de tarea, el comportamiento que entrega y su evidencia. Otro integrante revisa. Se integra cuando pasa `Pruebas`, existe la aprobación requerida y las conversaciones están resueltas.

En **Settings → Branches → Add branch protection rule**, aplicar a `main`: requerir PR, una aprobación, status check `Pruebas`, conversaciones resueltas y aplicar las restricciones también a administradores. Mantener desactivados los permisos de force push y borrado. El check aparece como opción después de que el workflow se haya ejecutado. La protección de ramas está disponible en repositorios públicos con GitHub Free; los privados requieren un plan compatible. [Documentación de GitHub](https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/managing-protected-branches/about-protected-branches).

## T0.2 y T0.3 · Render

1. Verificar que el repositorio remoto contiene `render.yaml`, `package-lock.json`, código, esquema y seed. Ejecutar `npm ci` y `npm test` localmente.
2. Entrar en Render con la cuenta elegida por el propietario y conectar GitHub con acceso a ese repositorio. Seleccionar **New → Blueprint** e importar el repositorio.
3. Revisar antes de aplicar: servicio web Node.js 24, base PostgreSQL, ambos con `plan: free`, misma región, `npm ci` como build y `npm start` como arranque. `DATABASE_URL` debe referenciar la base con `fromDatabase` y `property: connectionString`; no pegar una contraseña en el YAML. Es el mecanismo oficial de [Blueprints](https://render.com/docs/blueprint-spec).
4. Aplicar el Blueprint y esperar a que el servicio esté `Live`. Si Render indica que ya existe una base gratuita en el workspace, revisar el recurso existente antes de crear otro. Registrar el nombre de la base y la fecha de creación.
5. Inicializar tablas y cargar el catálogo mediante el mecanismo del proyecto. Si se ejecutan `npm run db:init` y `npm run db:seed` desde el equipo local, usar la conexión externa privada de PostgreSQL en `DATABASE_URL`; retirar la variable de la sesión después. Render Free no ofrece shell/SSH ni trabajos one-off. No depender de esos recursos para preparar la base.
6. Abrir la URL asignada, comprobar health y `GET /api/maquinaria`, y crear/consultar un contrato. Repetir desde otro equipo o una conexión distinta. Registrar evidencia sin credenciales.
7. Confirmar que el servicio sigue la rama `main` y que el despliegue automático está habilitado. Integrar un cambio aprobado mediante PR y registrar el despliegue resultante. La referencia de Blueprint documenta `autoDeployTrigger: checksPass` para desplegar cuando los checks pasan. [Referencia oficial](https://render.com/docs/blueprint-spec).

La UI y la API comparten origen: publicar el servicio web publica ambas. En la nube los contratos deben usar PostgreSQL, porque el sistema de archivos del servicio es efímero; PGlite queda para el desarrollo local.

## Límites del plan gratuito

Render documenta suspensión del servicio web después de 15 minutos sin tráfico y reactivación de aproximadamente un minuto. Cada workspace dispone de 750 horas mensuales de servicio gratuito. PostgreSQL Free admite una instancia por workspace, 1 GB, expira a los 30 días y no incluye backups. Preparar la demo con anticipación y exportar los datos que se quieran conservar antes de la expiración. Consultar uso y fecha de expiración en el Dashboard. [Límites oficiales de Render](https://render.com/docs/free), consultados el 6 de octubre de 2026.

## Secretos y evidencia

`DATABASE_URL`/connection string puede contener usuario y contraseña. Configurar el valor real en el entorno privado del servicio o en el `.env` local ignorado por Git. Compartirlo con el equipo por un canal privado; en la hoja escribir «conexión configurada y compartida privadamente», el nombre del recurso y evidencia sin el secreto. Si una credencial se publica por accidente, rotarla en el proveedor y retirar el valor expuesto.

El registro de despliegue debe contener URL pública, commit desplegado, enlace a `Pruebas`, fecha/hora de verificación, endpoint probado, resultado y persona que comprobó desde fuera. La cuenta, aprobación y prueba cruzada sólo se atribuyen a quien realmente las realizó.
