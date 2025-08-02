# Análisis de datos Telecom X

Tabla de contenido

1. **[Problemática](#Problemática)**
1. **[Tratamiento de Datos](#Tratamiento_de_Datos)**
1. **[Análisis Exploratorio de Datos](#Análisis_Exploratorio_de_Datos)**
1. **[Conclusión](#Conclusión)**
1. **[Recomendación](#Recomendación)**
1. **[Instrucciones para Ejecutar el Notebook](#Instrucciones_para_Ejecutar_el_Notebook)**

## **Problemática**

La **evasión de clientes**, conocida también como *Churn* simboliza un gran desafío para las empresas de servicios, especialmente en sectores competitivos como las telecomunicaciones. La pérdida de clientes no solo impica la disminución de ingresos, sino también costos asociados a la adquisición de nuevos suscriptores. El presente análisis posee como objetivo identificar y comprender los factores claves que influyen en la decisión de los clientes de cancelar su servicio, utilizando técnicas de análisis exploratorios de datos (EDA), buscaremos descubrir patrones y relaciones en los datos que puedan arrojar luz sobre las razones detrás de la evasión y, en última instancia, ayudar a desarrollar estrategias para retener a los clientes. 

## **Tratamiento de Datos**

El proceso de análisis empiezá extrayendo los datos desde un archivo JSON remoto para posteriormente preparar el dataset para el análisis. Los pasos clave incluyeron:

- **Carga y Normalización:** Los datos fueron cargados desde la URL proporcionada y normalizados para crear una estructura tabular manejable con Pandas.

- **Inspección Inicial:** Se revisaron las primeras y últimas filas, la información general (`.info()`), la presencia de valores nulos (`.isnull().sum()`) y filas duplicadas (`.duplicated().sum()`) para obtener una visión inicial de la calidad de los datos.

- **Revisión de Tipos de Datos:** Se examinaron los tipos de datos de cada columna (`.dtypes`) para identificar posibles inconsistencias.

- **Transformación de Variables Booleanas:** Las columnas que representaban valores booleanos ('Yes'/'No') fueron transformadas a un formato numérico (1 para 'Yes', 0 para 'No') para facilitar el análisis cuantitativo. Se manejaron los valores faltantes o inconsistentes durante esta transformación.

- **Conversión de Tipos Específicos:** Se identificó que la columna de 'Cargos_Totales' estaba como tipo 'object' debido a la presencia de posibles valores no numéricos (como cadenas vacías). Se convirtió a tipo numérico utilizando `pd.to_numeric` con `errors='coerce'` para convertir los valores problemáticos a `NaN`.

- **Creación de Nueva Variable:** Se calculó una nueva variable, 'Cuentas_Diarias' (Cargos Diarios), dividiendo los cargos mensuales por 30 y redondeando a tres decimales. Esto proporcionó una métrica de costo más granular.

- **Renombrado de Columnas:** Se renombraron las columnas para mejorar la legibilidad y comprensión de los datos en español.

- **Manejo de Valores Faltantes en 'Evasión':** Para los análisis que involucran la variable 'Evasión', se creó una copia del DataFrame (`df_clean`) donde se eliminaron las filas con valores nulos en esta columna, asegurando la integridad del análisis de evasión.

## **Análisis Exploratorio de Datos**

El análisis exploratorio de datos se centró en visualizar la distribución de la variable objetivo (Evasión) y explorar las relaciones entre la evasión y otras características de los clientes y sus servicios.

- **Distribución de la Evasión:** Un gráfico circular mostró la proporción de clientes que han evadido el servicio frente a los que permanecen activos. Esto proporcionó una base para entender la magnitud del problema del Churn.

- **Evasión por Variables Categóricas:** Se utilizaron gráficos de barras agrupados para visualizar la distribución de la evasión en función de variables categóricas clave como 'Género', 'Tipo_Contrato', 'Método_Pago' y 'Servicio_Internet'. Estos gráficos permitieron identificar qué categorías dentro de estas variables presentan mayores tasas de evasión. Por ejemplo, se observó si ciertos tipos de contrato o métodos de pago están más asociados con la baja de clientes.

- **Análisis Descriptivo de Variables Numéricas:** Se calculó y presentó un resumen estadístico descriptivo de las variables numéricas (Conteo, Media, Desviación Estándar, Mínimo, Cuartiles, Máximo), renombrándolo para mayor claridad. Esto proporcionó una comprensión cuantitativa de la distribución de estas variables.

- **Correlación entre Variables Numéricas:** Se calculó y visualizó una matriz de correlación entre todas las variables numéricas del dataset. Este mapa de calor permitió identificar la fuerza y dirección de las relaciones lineales entre pares de variables, incluyendo la correlación con la variable 'Evasión'.

- **Relación entre Cargos Diarios y Evasión:** Un gráfico de dispersión exploró visualmente la relación entre los cargos diarios y la evasión.

- **Relación entre Cantidad de Servicios y Evasión:** Para investigar si la cantidad de servicios contratados influye en la evasión, se creó una variable que suma los servicios numéricos. Se utilizaron boxplots para comparar la distribución de la cantidad de servicios entre clientes activos y los que evadieron, y un gráfico de barras para visualizar la tasa de evasión promedio por cantidad de servicios.

Estos análisis visuales y cuantitativos son fundamentales para identificar patrones y características de los clientes que tienden a evadir el servicio.

## **Conclusión**

A partir del análisis exploratorio de datos, se pueden extraer varias conclusiones clave:

- **Tasas de Evasión:** El gráfico circular reveló la proporción actual de clientes que han evadido, proporcionando una métrica clara del problema a abordar.

- **Impacto de Variables Categóricas:** Los gráficos de barras por categoría probablemente señalaron que ciertos grupos de clientes (por ejemplo, aquellos con un tipo de contrato específico, método de pago o servicio de internet) tienen una tasa de evasión notablemente mayor. Estos segmentos representan áreas de enfoque prioritario para las estrategias de retención.

- **Correlaciones Relevantes:** La matriz de correlación y los gráficos de dispersión/boxplot para variables numéricas ayudaron a identificar qué características numéricas (como los cargos mensuales o la tenencia) están más fuertemente correlacionadas con la evasión. Por ejemplo, una alta correlación positiva entre "Cargos_Mensuales" y "Evasión" sugeriría que los clientes con facturas más altas son más propensos a irse. La exploración de la relación entre "Cargos_Diarios" y "Cantidad_Servicios" con la evasión proporcionó insights adicionales sobre cómo el costo y la amplitud de los servicios afectan la decisión del cliente.

Los insights obtenidos de este análisis visual y cuantitativo son cruciales para comprender el perfil del cliente que evade y los factores que contribuyen a esta decisión. Esta información puede ser utilizada para segmentar a los clientes en riesgo y diseñar intervenciones dirigidas.

# **Recomendación**

Basado en los hallazgos de este análisis, se sugieren las siguientes recomendaciones estratégicas para reducir la evasión de clientes:

- **Segmentación de Clientes en Riesgo:** Utilizar las características identificadas (como tipo de contrato, método de pago, servicio de internet y potencialmente los cargos mensuales/diarios) para crear modelos que predigan qué clientes tienen una alta probabilidad de evadir.

- **Estrategias de Retención Dirigidas:** Implementar programas de retención específicos para los segmentos de clientes identificados como de alto riesgo. Esto podría incluir ofertas personalizadas, mejoras en el servicio al cliente, o comunicaciones proactivas para abordar sus preocupaciones.

- **Optimización de la Oferta de Servicios:** Analizar si la cantidad de servicios contratados o los cargos asociados están contribuyendo a la evasión. Considerar la posibilidad de ofrecer paquetes de servicios más atractivos o ajustar las estructuras de precios para segmentos vulnerables.

- **Mejora en la Experiencia del Cliente:** Si el análisis sugiere que ciertos métodos de pago o tipos de contrato están asociados con una mayor evasión, investigar las razones subyacentes. Podría ser necesario mejorar la facilidad de uso de ciertos métodos de pago o la claridad de los términos del contrato.

- **Monitoreo Continuo:** Establecer un sistema para monitorear continuamente las métricas de evasión y los factores que la influyen. El análisis de datos debe ser un proceso iterativo que permita ajustar las estrategias de retención a medida que cambian las dinámicas del mercado y el comportamiento del cliente.

La implementación de estas recomendaciones, respaldada por un análisis de datos sólido, puede ayudar a Telecom X a reducir su tasa de evasión y mejorar la rentabilidad a largo plazo.

# **Instrucciones para Ejecutar el Notebook**

1. Clona este repositorio:

   ```bash
   git clone https://github.com/usuario/proyecto-telecomx.git
   cd proyecto-telecomx

2. Instala las dependencias:

   ```bash
   pip install -r requirements.txt

3. Abre el notebook:

  ```bash
  jupyter notebook TelecomX.ipynb
  ```

|💡 Los datos se cargan automáticamente desde una URL pública, por lo que no es necesario descargar archivos adicionales
