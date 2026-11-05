# Tablero de Productividad · Grupo Río

Repositorio del tablero semanal de productividad de Grupo Río.

## Contenido

| Archivo | Descripción |
|---|---|
| `Tablero_GrupoRio_Julio.html` | Tablero autocontenido (HTML + CSS + JS en línea, con iframe de Estudios vía `srcdoc`). Última versión de referencia. |
| `propuestas/` | 3 prototipos de rediseño a pantalla completa (ver `propuestas/README.md`). |
| `INSTRUCCIONES_Actualizacion_Semanal.md` | Flujo para actualizar el tablero con los archivos de cada semana (Indicador, Interpretación, Transcripción, Efectividad). |

## Uso

El tablero es un único archivo `.html` que se abre directamente en el navegador. Usa el **diseño B**
(elegido de `propuestas/`): barra superior con pestañas, ancho completo, botón de pantalla completa,
y las gráficas ya vienen cargadas con todas las sucursales y modalidades.

Vistas: Resumen (tarjetas por sucursal y por modalidad, volumen, tiempos del proceso, chequeos),
Indicador (mapas de calor de todas las sucursales y matriz modalidad × sucursal, más el detalle por unidad),
Chequeos médicos, Productividad, Efectividad, Volumen de estudios (iframe), Promesa y Cumplimiento,
2026 vs 2025 y Proyectos.

## Actualización semanal

Para cargar una nueva semana, seguir el flujo descrito en
[`INSTRUCCIONES_Actualizacion_Semanal.md`](INSTRUCCIONES_Actualizacion_Semanal.md).
Se parte siempre de la última versión del HTML publicada en este repositorio; **no** se
reconstruye de memoria.
