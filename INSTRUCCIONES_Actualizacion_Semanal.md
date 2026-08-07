# Actualización semanal — Tablero Grupo Río

Claude: cuando el usuario suba archivos con este documento, ejecuta el flujo de abajo directamente. **No repases todo el tablero ni releas todas las constantes.** Ya conoces la estructura; solo aplica los cambios de la nueva semana N.

---

## 1. Archivos que subo (todos por el chat)

| Qué | Nombre típico | Para qué |
|---|---|---|
| Indicador semanal | `Semana N.csv` | Indicador por unidad de la semana |
| Interpretación | `Exa_Semana_N.csv` | radiologos, modalidad, sedes |
| Transcripción | `Sio_Semana_N.csv` | transcriptores, servicios, tendencias |
| Producción radiólogos (5 CSV/xlsx) | nombres de radiólogos | efectividad (errores del mes) |

Si algún archivo falta, sáltate esa parte y avísame al final (no la inventes).

**El tablero de trabajo está en `/home/claude/tablero.html`.** Si no existe (contenedor reseteado), pídeme el HTML más reciente o dime que lo suba; NO lo reconstruyas de memoria.

---

## 2. Indicador (constante `unidades` NO se toca — es acumulado anual)

Del `Semana N.csv` (header en fila 8, layout 46 campos: `est`=3, `dep`=4, `fp`=8 Promesa[A], `fb`=10 Agenda[B], `A-F`=42, `Sucursal`=45):

- **Cumplimiento**: un estudio incumple si **columna 42 (A-F horas) < 0**. Parsear formato `h:mm` y decimal.
- Verificar que el total cuadre con el encabezado (filas 3-6: Prometidos / Cumplimiento real / Incumplimiento). **Usa el CSV fuente, NO el PDF** (el PDF arrastra valores de la semana previa).
- Calcular indicador por unidad (col 45 Sucursal) y por depto (col 4).

**Aplicar en `tablero.html`:**
- `indTemporal.semana`: append `"SN"` a `p`, y el indicador de cada unidad al array `u[unidad]` (unidades sin dato → `null`).
- `deptEvo`: append `"SN"` a `semanas`; para cada depto append su `sem` (ind%) y `semT` (total); deptos sin dato → `sem:null, semT:0`.
- `trSems`: append `"SN"`.
- Textos/comparativas: `S(N-1) vs S(N-2)` → `SN vs S(N-1)`; rangos `S2–S(N-1)` → `S2–SN`; "Semana en curso: S(N-1)" → `SN` con sus fechas; notas "S2–S(N-1)" y "S28 a S(N-1)".
- **NO** tocar `chqSerie` salvo que suba un archivo de chequeos de la semana N.

Normalización de nombres (mojibake del CSV → tablero): `López Mateos`, `Clínica de la Mujer`, `Las Águilas`. Deptos: `Tomografía Axial C.`, `Electromiografía y P.E.`, `EEG y Mapeo Cerebral`, etc.

## 3. Interpretación (reemplazar S(N-1) → SN)

Del `Exa_Semana_N.csv` (jerárquico: User → Facility → Modality → fecha, con Study Count):
- `radiologos`: nombre corto `Apellido, Nombre` con su total.
- `modalidad`: sumar por MR/CT/US.
- `sedes`: sumar por Facility (López Mateos, Chamizal, Acueducto…).
- Badge "Semana N · fechas" y texto "Distribución de los X estudios" (X = total interpretación).
- `trendInterp`: append `{w:'SN',v:TOTAL}`.

## 4. Transcripción (reemplazar S(N-1) → SN)

Del `Sio_Semana_N.csv` (fila `Total` por usuario; la semana suele cruzar meses → sumar bloque mes1 + mes2 por usuario):
- `transcriptores`: top 12 por total + `{name:'Otros',v:resto}`.
- `servicios`: total por depto (última columna de cada fila de depto).
- `trendTrans`: append `{w:'SN',v:TOTAL}`.
- Badges y notas de rango de semanas.

## 5. Efectividad (mantener fuente oficial)

De los 5 CSV de radiólogos: solo algunos traen columnas de error (`INCONSISTENCIA MENOR`, `ORTOGRAFÍA`, `INCONSISTENCIA GRAVE`). 
- **Por defecto**: `effMes` mantiene el valor oficial del mes cerrado y agrega el mes en curso = 0. NO mezclar auto-registros con la hoja oficial salvo que yo lo pida.
- Puedo pedirte los denominadores de producción del mes (contar citas numéricas por radiólogo) si vamos a cerrar la efectividad del mes.

## 6. Estudios (iframe) — normalmente NO se toca

El dataset `DATA` del iframe cubre ene–26 jul 2026 por hora/unidad. Solo se actualiza si subo CSV mensuales nuevos que extiendan esa ventana. Una semana suelta del indicador NO va aquí.

## 7. Validación y entrega (siempre)

1. Validar sintaxis: extraer los 2 `<script>` externos (excluyendo el `srcdoc` del iframe) y `node --check` cada uno.
2. Si toqué el iframe: editar `/home/claude/iframe_content.html` desescapado → re-escapar (`&`→`&amp;`, `"`→`&quot;`, `<`→`&lt;`, `>`→`&gt;`, en ese orden) → re-inyectar al `srcdoc` vía regex `(<iframe class="est-frame" title="Estudios Grupo Río" srcdoc=")(.*?)("></iframe>)`.
3. Prueba headless Puppeteer (chrome en `/home/claude/.cache/puppeteer/chrome/linux-131.0.6778.204/chrome-linux64/chrome`, args `['--no-sandbox']`, vía `require('/home/claude/.npm-global/lib/node_modules/@mermaid-js/mermaid-cli/node_modules/puppeteer')`): recorrer las 8 vistas, confirmar `ERRORES: NINGUNO` y que `indTemporal.semana.p`, `trSems`, `trendTrans` incluyan SN.
4. Copiar a `/mnt/user-data/outputs/Tablero_GrupoRio_SemanaN.html` y `present_files`.

## 8. Estilo de trabajo

- Español, respuestas concisas.
- No repasar el dashboard completo ni volcar constantes grandes.
- Aplicar los cambios de una, validar, entregar. Solo preguntar si un dato no cuadra o falta un archivo.
