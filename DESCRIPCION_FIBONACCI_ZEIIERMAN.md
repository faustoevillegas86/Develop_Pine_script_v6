# Descripción detallada — Fibonacci Projection with Volume & Delta Profile (Zeiierman)

> **Nota de alcance**: Esta descripción se deriva **exclusivamente del código local** del indicador y sus parámetros expuestos. No se incluye ningún resultado de backtesting ni recomendaciones óptimas basadas en datos de mercado. Las sugerencias de ajuste por tipo de activo se presentan como **rangos de uso razonables** según la lógica interna del script y deben validarse por el usuario en TradingView. 

## 1) ¿Qué hace el indicador?

El script identifica los **últimos swings** (máximo y mínimo relevantes) usando un período configurable (`Period`). Con esos swings construye:

1. **Niveles de retroceso de Fibonacci** (0.236, 0.382, 0.5, 0.618, 0.786) entre el último swing alto y bajo, dibujados como líneas horizontales con etiquetas opcionales. 【F:CODIGOS/Fibonacci Projection with Volume & Delta Profile (Zeiierman).pine†L35-L217】【F:CODIGOS/Fibonacci Projection with Volume & Delta Profile (Zeiierman).pine†L520-L589】
2. **Proyección de movimientos futuros** basada en un nivel de proyección seleccionado (`Projection Level`). Se calculan segmentos proyectados hacia adelante, cajas de nivel y etiquetas con el % de cambio entre cada tramo. 【F:CODIGOS/Fibonacci Projection with Volume & Delta Profile (Zeiierman).pine†L101-L119】【F:CODIGOS/Fibonacci Projection with Volume & Delta Profile (Zeiierman).pine†L590-L717】
3. **Perfil de volumen dentro del rango del swing** (Fib Volume Profile): un histograma de volumen por rangos de precio (filas/bins), dividido en volumen alcista y bajista. Se pinta en forma de cajas apiladas dentro del rango del swing. 【F:CODIGOS/Fibonacci Projection with Volume & Delta Profile (Zeiierman).pine†L165-L214】【F:CODIGOS/Fibonacci Projection with Volume & Delta Profile (Zeiierman).pine†L721-L831】
4. **Perfil de delta de volumen por bandas Fibonacci** (Fib Volume Delta): suma el volumen alcista y bajista por bandas entre niveles Fibonacci y calcula el delta (bull - bear), mostrando cajas de ancho proporcional al delta. 【F:CODIGOS/Fibonacci Projection with Volume & Delta Profile (Zeiierman).pine†L216-L259】【F:CODIGOS/Fibonacci Projection with Volume & Delta Profile (Zeiierman).pine†L833-L920】

## 2) Cómo interpretar el indicador

- **Swings (Period)**: El período controla el tamaño del swing. Períodos más grandes producen swings menos frecuentes (mayor estabilidad) y más pequeños producen swings más sensibles (mayor ruido). 【F:CODIGOS/Fibonacci Projection with Volume & Delta Profile (Zeiierman).pine†L52-L71】【F:CODIGOS/Fibonacci Projection with Volume & Delta Profile (Zeiierman).pine†L457-L476】
- **Niveles de Fibonacci**: Actúan como zonas probables de reacción del precio dentro del swing vigente. Son líneas horizontales dinámicas que se actualizan con cada nuevo swing. 【F:CODIGOS/Fibonacci Projection with Volume & Delta Profile (Zeiierman).pine†L520-L589】
- **Proyección**: El script proyecta tramos futuros partiendo de la estructura del swing actual y el nivel `Projection Level`, añadiendo una extensión adicional (`1.272`) como tramo final. Se muestran porcentajes de cambio por tramo y cajas con el nivel proyectado. 【F:CODIGOS/Fibonacci Projection with Volume & Delta Profile (Zeiierman).pine†L590-L717】
- **Perfil de volumen (Fib Volume Profile)**: Distribuye el volumen total del swing en filas de precio. Se puede invertir el orden bull/bear y ajustar el número de filas (más filas = más detalle, más carga). 【F:CODIGOS/Fibonacci Projection with Volume & Delta Profile (Zeiierman).pine†L165-L214】【F:CODIGOS/Fibonacci Projection with Volume & Delta Profile (Zeiierman).pine†L721-L831】
- **Perfil de delta (Fib Volume Delta)**: Detecta zonas donde el volumen alcista supera al bajista (delta positivo) y viceversa. El ancho de cada caja representa la magnitud del delta. 【F:CODIGOS/Fibonacci Projection with Volume & Delta Profile (Zeiierman).pine†L216-L259】【F:CODIGOS/Fibonacci Projection with Volume & Delta Profile (Zeiierman).pine†L833-L920】

## 3) Parámetros de ajuste (qué controlan y cuándo usarlos)

### Núcleo del indicador
- **Period**: tamaño del swing. Valores altos = swings más “limpios” pero menos frecuentes. Valores bajos = mayor sensibilidad. 【F:CODIGOS/Fibonacci Projection with Volume & Delta Profile (Zeiierman).pine†L52-L71】【F:CODIGOS/Fibonacci Projection with Volume & Delta Profile (Zeiierman).pine†L457-L476】
- **Projection Level**: nivel Fibonacci para la proyección (0.236, 0.382, 0.5, 0.618, 0.786). Ajusta la pendiente/altura de los tramos proyectados. 【F:CODIGOS/Fibonacci Projection with Volume & Delta Profile (Zeiierman).pine†L58-L66】【F:CODIGOS/Fibonacci Projection with Volume & Delta Profile (Zeiierman).pine†L590-L651】

### Estilo visual (Fib Levels, Projection, Boxes)
- Colores, grosor de líneas y tamaño de texto son configurables para adaptar visibilidad. 【F:CODIGOS/Fibonacci Projection with Volume & Delta Profile (Zeiierman).pine†L68-L358】

### Performance Free (TradingView Free)
- **Mostrar histórico**: al desactivarlo, el perfil de volumen/delta se restringe al rango visible para reducir carga. 【F:CODIGOS/Fibonacci Projection with Volume & Delta Profile (Zeiierman).pine†L120-L151】【F:CODIGOS/Fibonacci Projection with Volume & Delta Profile (Zeiierman).pine†L760-L771】
- **Rango visible**: limita el cálculo a las últimas N barras. 【F:CODIGOS/Fibonacci Projection with Volume & Delta Profile (Zeiierman).pine†L126-L134】【F:CODIGOS/Fibonacci Projection with Volume & Delta Profile (Zeiierman).pine†L760-L771】
- **Máx barras perfil**: límite estricto de barras procesadas (loop). 【F:CODIGOS/Fibonacci Projection with Volume & Delta Profile (Zeiierman).pine†L137-L145】【F:CODIGOS/Fibonacci Projection with Volume & Delta Profile (Zeiierman).pine†L765-L771】

### Fib Volume Profile
- **Rows**: detalle del perfil (más filas = más granularidad, más carga). 【F:CODIGOS/Fibonacci Projection with Volume & Delta Profile (Zeiierman).pine†L169-L187】【F:CODIGOS/Fibonacci Projection with Volume & Delta Profile (Zeiierman).pine†L741-L758】
- **Flip Bull/Bear**: invierte el orden lateral del volumen alcista y bajista. 【F:CODIGOS/Fibonacci Projection with Volume & Delta Profile (Zeiierman).pine†L180-L187】【F:CODIGOS/Fibonacci Projection with Volume & Delta Profile (Zeiierman).pine†L789-L807】

### Fib Volume Delta
- **Max Width**: ancho máximo (en barras) para escalar el delta. 【F:CODIGOS/Fibonacci Projection with Volume & Delta Profile (Zeiierman).pine†L227-L238】【F:CODIGOS/Fibonacci Projection with Volume & Delta Profile (Zeiierman).pine†L881-L909】

## 4) Presets por tipo de ticker (con fundamentos, no optimizados)

> **Importante**: El script no incluye lógica específica por ticker y no hay resultados empíricos adjuntos. Los presets de abajo se basan **solo en cómo el indicador reacciona al tamaño del swing y la granularidad del perfil**, por lo que **deben validarse en TradingView** para cada activo/temporalidad.

### Presets (parámetros sugeridos)

| Tipo de ticker | Period | Projection Level | Rows (perfil) | Max Width (delta) | Temporalidades sugeridas |
| --- | --- | --- | --- | --- | --- |
| **Cripto majors / Forex (alta liquidez)** | 80–150 | 0.5–0.618 | 8–16 | 20–40 | 1H–4H (15m–30m si se requiere sensibilidad) |
| **Cripto alt/meme (alta volatilidad)** | 100–200 | 0.618–0.786 | 6–12 | 20–30 | 2H–1D |
| **Acciones/ETFs (liquidez variable)** | 60–120 (hasta 150 en baja liquidez) | 0.382–0.618 | 8–20 | 20–35 | 1H–1D (más estable 4H–1D) |
| **Bonos (baja volatilidad)** | 120–200 | 0.382–0.5 | 6–10 | 15–25 | 4H–1D |

### Fundamentos de estos presets (cómo afectan la lógica del script)

- **Period (tamaño del swing)**: A mayor volatilidad o ruido, se recomienda **subir Period** para evitar swings demasiado frecuentes. En activos más estables se puede usar Period menor para capturar movimientos más finos. Esto mantiene consistente la detección de `hi`/`lo` y por tanto los niveles Fibonacci y proyecciones. 【F:CODIGOS/Fibonacci Projection with Volume & Delta Profile (Zeiierman).pine†L52-L71】【F:CODIGOS/Fibonacci Projection with Volume & Delta Profile (Zeiierman).pine†L457-L476】
- **Projection Level**: En activos muy volátiles suele usarse 0.618–0.786 para reflejar extensiones más amplias del swing, mientras que en activos más estables 0.382–0.5 reduce sobre-proyección. Esto impacta directamente los segmentos `fibb`/`fibb2` y la extensión final `1.272`. 【F:CODIGOS/Fibonacci Projection with Volume & Delta Profile (Zeiierman).pine†L58-L66】【F:CODIGOS/Fibonacci Projection with Volume & Delta Profile (Zeiierman).pine†L590-L651】
- **Rows (perfil)**: Más filas = mayor granularidad, pero mayor carga y más sensibilidad a micro-variaciones de precio. En activos con mucho ruido, menos filas ayuda a estabilizar el perfil. 【F:CODIGOS/Fibonacci Projection with Volume & Delta Profile (Zeiierman).pine†L169-L187】【F:CODIGOS/Fibonacci Projection with Volume & Delta Profile (Zeiierman).pine†L741-L758】
- **Max Width (delta)**: Ajusta el ancho máximo de cajas del delta por banda. En mercados más líquidos puede ampliarse para destacar desequilibrios; en activos con baja liquidez se recomienda moderarlo para evitar dominancias visuales exageradas. 【F:CODIGOS/Fibonacci Projection with Volume & Delta Profile (Zeiierman).pine†L227-L238】【F:CODIGOS/Fibonacci Projection with Volume & Delta Profile (Zeiierman).pine†L881-L909】

## 5) Buenas prácticas de publicación en TradingView

- Describirlo como **indicador visual** basado en swings y niveles Fibonacci con proyección, acompañado de perfiles de volumen y delta opcionales. 【F:CODIGOS/Fibonacci Projection with Volume & Delta Profile (Zeiierman).pine†L52-L259】【F:CODIGOS/Fibonacci Projection with Volume & Delta Profile (Zeiierman).pine†L520-L920】
- Sugerir el uso de **Performance Free** para evitar cargas en cuentas Free cuando se usan perfiles. 【F:CODIGOS/Fibonacci Projection with Volume & Delta Profile (Zeiierman).pine†L120-L151】【F:CODIGOS/Fibonacci Projection with Volume & Delta Profile (Zeiierman).pine†L760-L771】
- Indicar que las proyecciones son **hipótesis basadas en el swing actual** y no constituyen señales de compra/venta.

