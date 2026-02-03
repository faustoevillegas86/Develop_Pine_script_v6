# Bitácora de calidad Pine Script v6

## Objetivo
Registrar controles para evitar errores de sintaxis, tipos, límites y rendimiento en TradingView Free.

## Checklist aplicado
- [x] `//@version=6` en línea 1 del script.
- [x] Uso de `indicator()` único con parámetros válidos.
- [x] `input.*()` con tipos correctos (`int/float/bool/color/string`).
- [x] `linewidth >= 1` en líneas.
- [x] Sin uso de `na` en variables `bool`.
- [x] Bucles capados a `<= 50` iteraciones en perfiles (Free).
- [x] Arrays dentro de límites razonables (sin >500 elementos).
- [x] Sin `request.security()` (0 llamadas).
- [x] Objetos limpiados (arrays de líneas/labels/boxes) para evitar acumulación.
- [x] Visuales pesados con toggles por defecto desactivados para Free.

## Errores prevenidos
- **Loops extensos**: se añadió `maxLoopBars` para limitar barras procesadas.
- **Sobrecarga visual**: `rows` max 30 y perfil desactivado por defecto.
- **Repaint visual**: proyección marcada como predictiva y aislada de perfiles históricos.
