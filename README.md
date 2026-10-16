# Memoria del proyecto - Yu Yu Hakusho (Genesis) / Makyo Toitsusen

Documentos de trabajo del reversing. **Todo el contenido sigue ahí; lo que cambió
es la separación por tema**, para que no haya que leer 8500 líneas de registro
después de cada compactación.

## Lo que se lee

| archivo | qué es | líneas |
|---|---|---|
| **`GENERAL/SISTEMAS.txt`** | las reglas del juego que valen para más de un personaje | 478 |
| **`GENERAL/PROYECTO.txt`** | dónde estamos, qué falta y en qué orden | 225 |
| **`GENERAL/METODO.txt`** | las lecciones de procedimiento | 1681 |

Ese es el orden de lectura después de una compactación: los dos primeros
enteros, y `HIT STATE.txt` solo si la ronda toca reacciones.

## Lo que no se lee entero

| archivo | qué es |
|---|---|
| `GENERAL/CONTEXTO.txt` | el archivo histórico, una sección por ronda |
| `GENERAL/HIT STATE.txt` | la tabla de reacciones y todos los estados |
| `GENERAL/MOVES DE TODOS.txt` | los 227 golpes del ROM (generado) |
| `GENERAL/AVANCE DECOMP.txt` | el peso de cada personaje en la ROM |
| `HIEI PDF/`, `KURAMA PDF/`, `SENSU PDF/` | un documento por personaje |

`CONTEXTO.txt` y `HIT STATE.txt` **no están en el repositorio**: son grandes y se
consultan con `grep`, no se leen. Están en la carpeta del proyecto.

## Reglas de escritura

- `.txt` en ASCII, sin BOM, saltos LF.
- Los `.LUA` **nunca** con `Set-Content`: mete BOM y rompe FBNeo.
  Usar `[System.IO.File]::WriteAllLines` con `UTF8Encoding($false)`.
- Los generadores producen, los documentos se editan a mano. Un hallazgo
  perdido no se vuelve a escribir.
- Copia en `_backup txt/` antes de tocar cualquier cosa.
- Un hallazgo va a **un** archivo de sistema; al registro solo una línea que
  diga dónde quedó.

## Lo que NO hace este proyecto

**Modificar la ROM.** No hay modding: solo análisis. Los `.LUA` son pasivos —
leen memoria y dibujan, pero **no escriben en la memoria del juego y no usan
`joypad.set`**.