# Auditoría institucional - Fibonacci Projection with Volume & Delta Profile (Zeiierman)

## 1) Auditoría exhaustiva (9 puntos)

### 1. Versión desarrollo
- El script declara `//@version=6` y usa `indicator()` con `overlay=true` y `max_bars_back=5000`. 【F:CODIGOS/Fibonacci Projection with Volume & Delta Profile (Zeiierman).pine†L4-L12】
- Validación documental: `indicator()` define propiedades globales y es obligatorio en indicadores. 【F:complete_reference.md†L8605-L8633】

### 2. Inventario técnico
- Variables `var` persistentes: tooltips `t1..t43`, líneas `hiLine/loLine`, arreglos de objetos (`fibbLines`, `fibbLabels`, `forecastLines`, `areas`, `perc`, `fibProfileBoxes`, `fibDeltaBoxes`) y `deltaStartX`. 【F:CODIGOS/Fibonacci Projection with Volume & Delta Profile (Zeiierman).pine†L14-L458】
- Inputs: parámetros de fib, estilos, performance Free (`showHistorical`, `visibleBars`, `maxLoopBars`) y perfiles de volumen/delta. 【F:CODIGOS/Fibonacci Projection with Volume & Delta Profile (Zeiierman).pine†L67-L247】
- Tipos: `array<line>`, `array<label>`, `array<box>`, `array<float>`, `array<int>` y tipos simples `int/float/bool/string/color`. 【F:CODIGOS/Fibonacci Projection with Volume & Delta Profile (Zeiierman).pine†L67-L744】
- Sin `import`, sin `map/matrix/enum/UDT`.

### 3. Lógica algoritmos
- **Swings**: `ta.highest/lowest`, `ta.barssince`, `ta.valuewhen` para precios y bar index. 【F:CODIGOS/Fibonacci Projection with Volume & Delta Profile (Zeiierman).pine†L418-L434】
- **Fibonacci retracement**: niveles `lvls` y cálculo con `fibbFunc()`, con líneas y labels opcionales. 【F:CODIGOS/Fibonacci Projection with Volume & Delta Profile (Zeiierman).pine†L486-L533】
- **Proyección**: 4 puntos (origen + 3 targets), segmentos futuros, cajas de nivel y labels percentuales. 【F:CODIGOS/Fibonacci Projection with Volume & Delta Profile (Zeiierman).pine†L535-L628】
- **Perfil de volumen**: bins entre swing high/low, acumula volumen bull/bear, normaliza y dibuja cajas con gradiente. Ahora se limita por `visibleBars` y `maxLoopBars`. 【F:CODIGOS/Fibonacci Projection with Volume & Delta Profile (Zeiierman).pine†L631-L713】
- **Delta profile**: bandas por niveles fib, delta bull/bear por banda y cajas con ancho proporcional; también limitado por rango visible y cap de barras. 【F:CODIGOS/Fibonacci Projection with Volume & Delta Profile (Zeiierman).pine†L715-L803】

### 4. Objetos visuales (conteo)
- Líneas: 2 swing lines + 5 fib lines + 3 líneas de proyección. 【F:CODIGOS/Fibonacci Projection with Volume & Delta Profile (Zeiierman).pine†L436-L628】
- Labels: hasta 5 fib labels + 3 labels de porcentaje. 【F:CODIGOS/Fibonacci Projection with Volume & Delta Profile (Zeiierman).pine†L510-L628】
- Boxes: proyección (hasta 3) + volumen por filas (hasta 2×rows) + delta por bandas. 【F:CODIGOS/Fibonacci Projection with Volume & Delta Profile (Zeiierman).pine†L585-L803】

### 5. Parámetros técnicos (inputs)
- Inputs críticos: `prd`, `lvl`, estilos, `showHistorical`, `visibleBars`, `maxLoopBars`, `rows`. 【F:CODIGOS/Fibonacci Projection with Volume & Delta Profile (Zeiierman).pine†L67-L247】
- Ajustes Free: `rows` max 30, loops de perfiles cap a 50 barras. 【F:CODIGOS/Fibonacci Projection with Volume & Delta Profile (Zeiierman).pine†L196-L214】【F:CODIGOS/Fibonacci Projection with Volume & Delta Profile (Zeiierman).pine†L666-L675】

### 6. Advertencias / errores potenciales
- `max_bars_back = 5000` incrementa buffers; se mantiene por compatibilidad histórica. 【F:CODIGOS/Fibonacci Projection with Volume & Delta Profile (Zeiierman).pine†L8-L12】
- Si `showHistorical=false`, los perfiles son aproximaciones al rango visible; no cambian la lógica del swing ni proyección, solo visualización y cálculo de perfiles. 【F:CODIGOS/Fibonacci Projection with Volume & Delta Profile (Zeiierman).pine†L188-L214】【F:CODIGOS/Fibonacci Projection with Volume & Delta Profile (Zeiierman).pine†L666-L675】

### 7. Repintado crítico
- **Repaint por swings**: `ta.highest/lowest` y `ta.valuewhen` pueden recalcular con nuevas barras. 【F:CODIGOS/Fibonacci Projection with Volume & Delta Profile (Zeiierman).pine†L418-L434】
- **Proyección futura intencional**: líneas y cajas se dibujan hacia `bar_index + 500`. 【F:CODIGOS/Fibonacci Projection with Volume & Delta Profile (Zeiierman).pine†L559-L603】

### 8. Integridad post (checklist)
- [x] orden
- [x] lógica
- [x] fórmulas
- [x] etiquetas
- [ ] alertas (no existen en el script)
- [x] plots/objetos
- [x] colores
- [x] inputs
- [x] scope
- [x] NA

### 9. Validación de discrepancias v6 vs previas
- Script ya en v6, sin migración requerida. No hay versión previa adjunta para comparar. 【F:CODIGOS/Fibonacci Projection with Volume & Delta Profile (Zeiierman).pine†L4-L803】

## 2) Validación documental (referencias oficiales usadas)
- `indicator()` para declaración global. 【F:complete_reference.md†L8605-L8633】
- Inputs tipados (`input.int`, `input.float`, `input.bool`, `input.color`, `input.string`). 【F:complete_reference.md†L8644-L8835】【F:complete_reference.md†L8772-L8808】【F:complete_reference.md†L9021-L9049】
- Swings: `ta.highest`, `ta.lowest`, `ta.barssince`, `ta.valuewhen`. 【F:complete_reference.md†L17238-L17259】【F:complete_reference.md†L17726-L17746】【F:complete_reference.md†L17923-L17944】【F:complete_reference.md†L18853-L18873】
- Objetos: `line.new`, `line.set_xy1/xy2`, `line.set_color`, `line.set_width`, `line.get_price`, `label.new`, `box.new`, `box.get_right`. 【F:complete_reference.md†L9947-L9979】【F:complete_reference.md†L10167-L10204】【F:complete_reference.md†L9985-L10000】【F:complete_reference.md†L10085-L10100】【F:complete_reference.md†L9804-L9819】【F:complete_reference.md†L9373-L9399】【F:complete_reference.md†L7370-L7401】【F:complete_reference.md†L7307-L7322】
- Arrays: `array.from`, `array.new_line`, `array.new_label`, `array.new_box`, `array.get`, `array.set`, `array.push`, `array.remove`, `array.size`, `array.copy`, `array.sort`. 【F:complete_reference.md†L5820-L5852】【F:complete_reference.md†L6441-L6456】【F:complete_reference.md†L6381-L6396】【F:complete_reference.md†L6261-L6276】【F:complete_reference.md†L5857-L5872】【F:complete_reference.md†L6774-L6790】【F:complete_reference.md†L6658-L6673】【F:complete_reference.md†L6718-L6730】【F:complete_reference.md†L6832-L6846】【F:complete_reference.md†L5681-L5695】【F:complete_reference.md†L6925-L6938】
- Colores y formato: `color.new`, `color.from_gradient`, `format.percent`, `format.volume`, `str.tostring`. 【F:complete_reference.md†L8001-L8028】【F:complete_reference.md†L8087-L8106】【F:complete_reference.md†L3224-L3234】【F:complete_reference.md†L3262-L3273】【F:complete_reference.md†L14875-L14899】
- `chart.point.from_index` y `barstate.isfirst`. 【F:complete_reference.md†L7884-L7899】【F:complete_reference.md†L22339-L22354】

## 3) Optimización institucional (6 puntos)
1. **Migración**: no requerida, ya en v6. Se reforzó documentación base. 【F:CODIGOS/Fibonacci Projection with Volume & Delta Profile (Zeiierman).pine†L1-L12】
2. **Sub-agente competitivo**: sin búsqueda externa (limitación local). Propuesta: mantener confluencias internas (swings + perfil + delta) pero con caps Free. 【F:CODIGOS/Fibonacci Projection with Volume & Delta Profile (Zeiierman).pine†L631-L803】
3. **Cálculos**: límites explícitos `visibleBars` y `maxLoopBars` reducen costo sin alterar lógica principal (swings/proyección). 【F:CODIGOS/Fibonacci Projection with Volume & Delta Profile (Zeiierman).pine†L188-L214】【F:CODIGOS/Fibonacci Projection with Volume & Delta Profile (Zeiierman).pine†L666-L675】
4. **Visuales**: `showFibProfile` por defecto `false`, `rows` max 30 para respetar límites Free. 【F:CODIGOS/Fibonacci Projection with Volume & Delta Profile (Zeiierman).pine†L188-L214】
5. **Repaint**: proyección se mantiene como visual, y se recomienda usar `showHistorical=false` para Free. 【F:CODIGOS/Fibonacci Projection with Volume & Delta Profile (Zeiierman).pine†L188-L214】【F:CODIGOS/Fibonacci Projection with Volume & Delta Profile (Zeiierman).pine†L559-L603】
6. **Rango visible**: implementado en perfiles de volumen/delta (no afecta swings ni proyección). 【F:CODIGOS/Fibonacci Projection with Volume & Delta Profile (Zeiierman).pine†L666-L675】【F:CODIGOS/Fibonacci Projection with Volume & Delta Profile (Zeiierman).pine†L751-L760】

## 4) Código (resumen + snippet)
- Código completo actualizado en: `CODIGOS/Fibonacci Projection with Volume & Delta Profile (Zeiierman).pine`.【F:CODIGOS/Fibonacci Projection with Volume & Delta Profile (Zeiierman).pine†L1-L803】

**Snippet (primeras 50 líneas):**
```pine
// This work is licensed under Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International
// https://creativecommons.org/licenses/by-nc-sa/4.0/
// © Zeiierman
// Base documental (Pine Script v6): indicator(), input.*, ta.*, line.*, label.*, box.*, array.*, color.*, chart.point.from_index() - ver complete_reference.md
//@version=6
indicator(
     "Fibonacci Projection with Volume & Delta Profile (Zeiierman)",
     shorttitle = "Fibonacci Projection (Zeiierman)",
     overlay = true,
     max_bars_back = 5000
     )
```
【F:CODIGOS/Fibonacci Projection with Volume & Delta Profile (Zeiierman).pine†L1-L12】

## 5) Mejoras cuantitativas (estimadas)
- **Cap de barras**: perfiles de volumen/delta procesan máximo 50 barras; reducción >80% vs swings largos. 【F:CODIGOS/Fibonacci Projection with Volume & Delta Profile (Zeiierman).pine†L666-L675】【F:CODIGOS/Fibonacci Projection with Volume & Delta Profile (Zeiierman).pine†L751-L760】
- **Reducción de boxes**: `rows` max 30 limita cajas a ~60 en perfil, evitando exceso. 【F:CODIGOS/Fibonacci Projection with Volume & Delta Profile (Zeiierman).pine†L196-L214】

## 6) Testing / validación
- No se ejecutaron pruebas automáticas; se recomienda validar en TradingView con 500 barras, `showHistorical=false` para Free. 【F:CODIGOS/Fibonacci Projection with Volume & Delta Profile (Zeiierman).pine†L188-L214】

## 7) Limitaciones
- El cap de barras puede suavizar el perfil en históricos; no afecta la proyección ni la detección de swings.
- Sin ejecución en TradingView, no se verificó compilación ni uso de memoria.

## 8) Recursos adicionales
- Documentación oficial Pine Script v6: `complete_reference.md`. 【F:complete_reference.md†L8605-L8633】
