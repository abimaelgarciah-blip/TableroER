# Propuestas de rediseño del tablero

Tres prototipos con los **datos reales** del tablero actual (corte S44 · octubre 2026).
Objetivo: pantalla completa, todas las sucursales y modalidades cargadas desde el inicio y el mínimo de clics.
Cada archivo es autocontenido; se abre directo en el navegador.

| Archivo | Idea | Clics para ver todo |
|---|---|---|
| `Propuesta_A_Centro_de_mando.html` | **Una sola pantalla sin scroll** (TV/monitor). KPIs arriba + 3 mapas de calor: sucursal × periodo, modalidad × periodo y modalidad × sucursal del mes, más chequeos. | 0 (1 clic opcional: Mensual ↔ 12 semanas) |
| `Propuesta_B_Pequenos_multiplos.html` | **Tarjetas, scroll vertical a lo ancho**. Una mini-gráfica por sucursal y por modalidad con la misma escala, volumen por sucursal y tiempos del proceso. | 0 (1 clic opcional: Mensual ↔ 16 semanas) |
| `Propuesta_C_Presentacion.html` | **Modo presentación por pestañas** (Indicador · Modalidades · Volumen · Tiempos · Chequeos), cada una a pantalla completa. Teclas 1–5 / ← →, y **Modo TV** que rota sola cada 20 s. | 0 en Modo TV; 1 clic por tema |

Común a las tres: botón **Pantalla completa**, tooltips con el valor exacto, meta 98% marcada,
colores fijos por sucursal, valor numérico siempre visible en los mapas de calor (no solo color) y modo oscuro automático.

Nota de datos: volumen mensual por sucursal llega a junio 2026 y el comparativo anual es septiembre (son los datos que
ya trae el tablero). Al elegir una propuesta se integra al `Tablero_GrupoRio_Julio.html` y al flujo semanal.
