# VERSIONS.json — Formato y mantenimiento

Este repositorio central (`Check_Versions_scripts`) usa un archivo JSON público para indicar la versión actual de cada recurso.

- Archivo esperado: `versions.json` (ruta: `main/versions.json`)
- Accesible vía RAW: `https://raw.githubusercontent.com/jgr-ry/Check_Versions_scripts/main/versions.json`

Formato mínimo (recomendado):

```json
{
  "JGR_Admin": "1.0.0",
  "": "1.0.0"
}
```

También se acepta la variante con objeto por entrada:

```json
{
  "JGR_Admin": { "version": "1.0.0", "url": "https://github.com/jgr-ry/JGR_Admin/releases/tag/v0.7.5" }
}
```

Buenas prácticas:
- Mantener la clave exactamente igual que `GetCurrentResourceName()` de cada recurso (ej. `JGR_Admin`).
- Incrementar la versión con formato semver (ej: `1.0.0`, `1.2.0`).
- Actualizar el archivo y hacer commit/push en `main` cada vez que publiques una release.

Uso en el script:
- El script usa `GetCurrentResourceName()` para buscar la clave y comparará la versión encontrada con la de `fxmanifest.lua`.
- Si la versión remota es mayor, se notificará en consola.

Si quieres, puedo crear un *pull request* ejemplo hacia `jgr-ry/Check_Versions_scripts` con este `versions.json` y `VERSIONS.md` (necesitaría acceso o que me confirmes que haga el PR desde mi fork).
