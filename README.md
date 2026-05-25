# Proyecto RappiPlus: de datos a decisiones de negocio

## Descripción del Proyecto

Este proyecto tiene como objetivo evaluar el desempeño del servicio **RappiPlus** para apoyar **decisiones de negocio basadas en datos**. Se utilizan múltiples datasets para realizar un análisis integral que cubre desde la calidad de los datos hasta la comunicación de resultados a través de un dashboard.

## Datasets Utilizados

- `rappiplus_orders_raw.csv`: Información de pedidos, precios, descuentos y revenue.
- `rappiplus_catalog.csv`: Costos de productos, categorías y proveedores.
- `rappiplus_marketing_spend.csv`: Inversión en marketing por canal y país.
- `events / users / user_activity (SQL)`: Comportamiento del usuario dentro de la plataforma (obtenido de una base de datos).
- `experiment_checkout_ui.csv`: Resultados de un experimento A/B en el checkout.

## Análisis y Estructura del Proyecto

El análisis se estructura en los siguientes pasos:

### 🔹 Paso 1: Cargar y validar la calidad de los datos

- **Objetivo**: Familiarizarse con la estructura de los datasets y asegurar su calidad para un análisis confiable.
- **Actividades**: Importación de librerías, carga de datasets (`orders`, `catalog`, `marketing`), exploración rápida (`.head()`, `.info()`, `.describe()`), conversión de tipos de datos (fechas), manejo de valores nulos (relleno con 'Desconocido'), estandarización de texto (ej. 'pais' a 'Title Case'), y eliminación de duplicados. Se verifica la consistencia de los montos totales.

### 🔹 Paso 2: Analizar si el negocio es rentable

- **Objetivo**: Calcular indicadores clave de rendimiento (KPIs) para evaluar ingresos, costos y rentabilidad del negocio.
- **Actividades**:
    - **Rentabilidad del negocio**: Cálculo del ingreso total (revenue), costo total de productos vendidos, inversión total en marketing y profit total. Determinación del margen de rentabilidad.
    - **Comportamiento de ventas**: Cálculo del ticket promedio por orden, cantidad promedio de productos por orden, identificación del producto más vendido y gasto en marketing por canal.
    - **Resumen Ejecutivo**: Análisis de concentración de ingresos por producto/categoría, comportamiento mensual y rendimiento por país.

### 🔹 Paso 3: Entender dónde se pierden los usuarios (funnel de conversión)

- **Objetivo**: Analizar el comportamiento de los usuarios en las distintas etapas del embudo de conversión para identificar puntos de fuga.
- **Actividades**: Conexión a la base de datos (PostgreSQL), exploración de la tabla `events`, construcción del funnel de usuarios únicos por evento y cálculo de las tasas de conversión paso a paso y desde el primer contacto (`first_visit`).

### 🔹 Paso 4: Evaluar si los usuarios regresan (retención por cohortes)

- **Objetivo**: Analizar la retención de usuarios para entender si regresan después de registrarse.
- **Actividades**: Exploración de las tablas `users` y `user_activity` de la base de datos, identificación de cohortes por mes de registro y cálculo de la retención semanal (usuarios activos en las semanas 1, 2 y 3).

### 🔹 Paso 5: Validar si los cambios generan impacto (test estadístico)

- **Objetivo**: Evaluar si una modificación en la UI del checkout impacta la tasa de conversión de compra mediante un experimento A/B.
- **Actividades**: Carga y análisis del dataset `experiment_checkout_ui.csv`, planteamiento de hipótesis nula y alternativa, aplicación de un Z-test para dos proporciones, y interpretación del valor p para determinar la significancia estadística de la diferencia observada. Visualización de las tasas de conversión con barras de error.

### 🔹 Paso 6: Comunicar los resultados (Dashboard en BI)

- **Objetivo**: Crear un dashboard interactivo que muestre de manera clara y visual los resultados del análisis.
- **Actividades**: Preparación de datos (carga de CSVs limpios, revisión de relaciones, creación de columnas calculadas y tabla de fechas), diseño de un Dashboard de Overview Ejecutivo (KPIs principales, evolución temporal, rendimiento por producto/categoría) y un Dashboard de Detalle/Drill-through (tabla de órdenes detallada, gráficos por producto, filtros).

## Conclusiones Clave

- RappiPlus es un negocio rentable con un margen de profit del 11.49%.
- Alta dependencia del producto 'Laptop-Gaming-16GB' y de la categoría 'Electrónica'.
- Argentina se destaca como el mercado más eficiente en términos de profit.
- Volatilidad mensual en los ingresos que sugiere la necesidad de investigar factores estacionales o campañas específicas.
- El experimento A/B en el checkout no mostró una diferencia estadísticamente significativa en la tasa de conversión, indicando que el cambio en la UI no tuvo un impacto positivo sustancial.
