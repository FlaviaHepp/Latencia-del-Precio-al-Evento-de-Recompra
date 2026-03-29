# 💰Latencia del Precio al Evento de Recompra

Validación de Ineficiencias y Arbitraje por País

## 📌Descripción

Este proyecto analiza qué tan rápido el mercado incorpora la información de una recompra de acciones en el precio.
Las recompras suelen ser eventos estructuralmente positivos, ya que reducen el float y señalan confianza del management.

Un mercado eficiente debería reflejar este impacto inmediatamente.
Si el precio sigue subiendo al día siguiente, puede indicar:
- Reacción tardía del mercado
- Subestimación inicial del evento
- Oportunidades de arbitraje sistemático

El análisis se realiza agregado por país / mercado, permitiendo comparar niveles de eficiencia entre jurisdicciones.

## 🧠Insight clave

- ¿En qué país los eventos de recompra generan el mayor rendimiento promedio al día siguiente?

Un rendimiento positivo y consistente post-evento sugiere:
- Ineficiencia informacional
- Menor cobertura analítica
- Potencial alpha explotable con estrategias event-driven

## 📊Valor de negocio

Este insight es útil para:

- Estrategias de arbitraje por eventos
Detectar mercados donde comprar el día del anuncio y vender al día siguiente es estadísticamente favorable.

- Comparación de eficiencia de mercado
Identificar qué países descuentan peor las recompras.

- Asignación geográfica de capital
Priorizar mercados con mayor persistencia del impacto positivo.

- Validación de hipótesis fundamental
Confirmar si las recompras realmente generan valor accionarial en distintas regiones.

## 🗂️Estructura de datos requerida

- eventos_corporativos
- ticker_id
- fecha
- tipo_evento (filtrado a 'Recompra_Acciones')
- precios_diarios
- ticker_id
- fecha
- close
- tickers
- ticker_id
- bolsa_mercado (país o mercado de cotización)

## ⚙️Lógica del análisis

- Identificación del evento
- Se seleccionan únicamente eventos de recompra de acciones.
-  Precio de referencia
- Se toma el precio de cierre el día del evento.

## 💼Reacción del mercado

Se obtiene el precio de cierre del día siguiente usando LEAD().

Cálculo del rendimiento

(Precio_día_siguiente - Precio_día_evento) / Precio_día_evento


## 🌎Agregación por país

Se calcula el rendimiento promedio post-evento por mercado.

Se filtran países con al menos 5 eventos para robustez estadística.

## 📈Interpretación de resultados

- Rendimiento promedio alto
- El mercado reacciona con retraso
- Posible oportunidad de arbitraje
- Rendimiento cercano a cero
- Alta eficiencia informacional
- El evento ya está completamente descontado

- Rendimiento negativo
- Recompras defensivas o interpretadas como señal de debilidad
- El ranking final ordena los países desde el más ineficiente al más eficiente.

## 🚀Posibles extensiones

- Comparar reacción inmediata (intraday) vs. cierre
- Analizar persistencia a 3 y 5 días
- Ajustar por tamaño de la recompra (% del market cap)
- Comparar recompras anunciadas vs. ejecutadas
- Construir un Índice de Eficiencia de Recompras por País

## 🧪Notas técnicas

Se recomienda indexar:
- eventos_corporativos (ticker_id, fecha, tipo_evento)
- precios_diarios (ticker_id, fecha)

El umbral de 5 eventos puede ajustarse según el universo analizado.

Ideal para backtesting en combinación con filtros de liquidez.

## 👤Autora
Flavia Hepp Proyecto de SQL aplicó un análisis de riesgo basado en eventos.

***
💡 **¿El mercado realmente descuenta rápido las recompras de acciones?**

Las recompras (*buybacks*) suelen interpretarse como una señal positiva: la empresa considera que su acción está infravalorada.
Pero… ¿el mercado reacciona de inmediato o hay margen para capturar valor al día siguiente?

👉 Analicé la **latencia del precio tras eventos de recompra**, midiendo el rendimiento del día siguiente al anuncio.

💥 **Insight clave:**
Hay mercados donde las recompras generan un **incremento significativo al día siguiente**, lo que sugiere que la reacción no es completamente instantánea… y podría haber oportunidades de arbitraje.

---

📊 **¿Qué evalué?**

* Eventos de *Recompra de Acciones*
* Precio de cierre el día del evento vs. día siguiente
* Rendimiento promedio por **bolsa/mercado de origen**
* Filtro de robustez: mínimo 5 eventos por mercado

---

🧠 **Interpretación:**

* Mercados con mayor retorno post-evento → posible **ineficiencia**
* Reacción tardía → oportunidad para estrategias *event-driven*
* Validación empírica del fenómeno tipo **post-announcement drift**

---

⚡ **¿Por qué importa?**

Porque incluso en señales “claras” como las recompras,
la velocidad de ajuste del mercado no es homogénea.

Y donde hay retrasos… hay estrategia.

---

📌 Pregunta abierta:
¿Han detectado *alpha* consistente operando eventos de recompra en ciertos mercados?

#QuantFinance #DataScience #StockMarket #Trading #SQL #Investing #Alpha #Analytics
