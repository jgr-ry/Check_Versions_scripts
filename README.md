# Check_Versions_scripts

Registro central de versiones de los scripts de FiveM **JGR** (jgr-ry). Cada script lleva el mismo comprobador (`server/version_check.lua`), que al arrancar el servidor lee este archivo y avisa en la consola si hay una versión más nueva.

- Archivo: [`versions.json`](versions.json)
- URL que consultan los scripts: `https://raw.githubusercontent.com/jgr-ry/Check_Versions_scripts/main/versions.json`

## Cómo funciona

1. El script lee su versión local de `version` en su `fxmanifest.lua`.
2. Descarga `versions.json` y busca su clave: el metadato `jgr_version_key` del fxmanifest (si no existe, el nombre de la carpeta del recurso).
3. Compara las versiones como semver real (1.10.0 es mayor que 1.9.0).
4. En consola muestra uno de estos avisos:
   - **Actualizado** (verde): tienes la última versión.
   - **Nueva versión disponible** (rojo): con tu versión, la última y el enlace de descarga (`repository` del fxmanifest).
   - **Versión de desarrollo**: tu versión local es más nueva que la publicada.

Los dueños de servidores pueden desactivar el aviso añadiendo esto a `server.cfg`:

```cfg
set jgr_versioncheck 0
```

## Formato de `versions.json`

El formato normal es `"clave": "versión"`:

```json
{
  "JGR_Admin": "1.1.0",
  "JGR_Flipcar": "1.2.0"
}
```

También se acepta un objeto por entrada, con enlace y notas de cambios opcionales:

```json
{
  "JGR_Admin": {
    "version": "1.1.0",
    "url": "https://github.com/jgr-ry/JGR_Admin/releases/tag/v1.1.0",
    "changelog": "Compatibilidad multi-framework y correcciones de seguridad"
  }
}
```

> Los comprobadores antiguos (anteriores a v2) solo entienden bien el formato de texto simple. Mientras haya servidores con versiones viejas, usa el formato `"clave": "versión"`.

## Metadatos en el `fxmanifest.lua` de cada script

```lua
version '1.1.0'
jgr_version_key 'JGR_Admin'                          -- clave en versions.json
repository 'https://github.com/jgr-ry/JGR_Admin'     -- enlace que se muestra al avisar

server_scripts {
    'server/version_check.lua',
    -- ...
}
```

## Publicar una versión nueva

1. Sube `version` en el `fxmanifest.lua` del script y añade la entrada al changelog de su README.
2. Fusiona el cambio del script en `main`.
3. **Después**, cambia aquí su versión en `versions.json` y haz commit en `main`.

Hazlo en ese orden: si `versions.json` se actualiza antes que el script, todos los servidores verán el aviso de una versión que aún no se puede descargar.

## Scripts registrados

| Clave | Versión |
|---|---|
| JGR_Admin | 1.1.0 |
| JGR_Antilag | 1.1.0 |
| JGR_Banking | 1.1.0 |
| JGR_Banking_no_modulos | 3.2.0 |
| JGR_Barber | 1.1.0 |
| JGR_CityHall | 1.1.0 |
| JGR_Dealership | 1.1.0 |
| JGR_Delivery | 1.1.0 |
| JGR_Doors | 1.1.0 |
| JGR_Flipcar | 1.2.0 |
| JGR_Graves | 1.1.0 |
| JGR_Hostage | 0.1.0 |
| JGR_IlegalSystem | 1.1.0 |
| JGR_KeySystem | 1.1.0 |
| JGR_Pausemenu | 1.1.0 |
| JGR_Radio | 1.0.0 |
| JGR_Reports | 1.1.0 |
| JGR_Shops | 1.1.0 |
| JGR_Trash | 1.1.0 |
| Antilag_System | 1.0.0 |
