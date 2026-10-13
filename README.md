# Análisis de clientes de ConnectaTel

## 1. Objetivo del proyecto

Este proyecto analiza el comportamiento de los clientes de **ConnectaTel**, una empresa de telecomunicaciones en Latinoamérica, con información registrada hasta 2024.

El objetivo es explorar y preparar los datos, construir un perfil estadístico de los usuarios, identificar patrones de uso y valores atípicos, y segmentar a los clientes según su edad y nivel de actividad. Los hallazgos sirven como punto de partida para proponer oportunidades comerciales, mejoras en los planes y acciones de retención.

## 2. Datasets utilizados

El notebook trabaja con tres archivos CSV:

| Archivo | Contenido principal | Uso en el análisis |
|---|---|---|
| `plans.csv` | Características de los planes, como precio, minutos y datos incluidos, y costos por consumo adicional. | Conocer la oferta disponible de ConnectaTel. |
| `users_latam.csv` | Información de los clientes, como edad, ciudad, fecha de registro, plan y datos relacionados con churn. | Explorar el perfil de los usuarios y limpiar valores inconsistentes. |
| `usage.csv` | Registros de uso de los servicios, incluidos llamadas y mensajes. | Calcular métricas de actividad por usuario. |

**Importante:** los CSV no están incrustados en el notebook. Para reproducir el análisis, es necesario obtenerlos de la fuente original del proyecto y colocarlos en una carpeta accesible. El notebook original usa las rutas `/datasets/plans.csv`, `/datasets/users_latam.csv` y `/datasets/usage.csv`; en otro entorno, estas rutas deben ajustarse.

## 3. Etapas del análisis

1. **Carga y exploración inicial:** importación de `pandas`, `numpy`, `seaborn` y `matplotlib`; lectura de los tres CSV; revisión de las primeras filas, dimensiones, tipos de datos y valores no nulos.
2. **Diagnóstico de calidad de datos:** recuento y proporción de valores ausentes; revisión de valores inválidos o sentinels, distribuciones y fechas.
3. **Limpieza básica:** tratamiento de edades inválidas mediante la mediana, sustitución de `?` en `city` por valores nulos y marcado como nulas de las fechas de registro de 2025 en adelante. También se examina la ausencia de datos en `duration` y `length` según el tipo de registro.
4. **Agregación por usuario:** cálculo de la cantidad de mensajes, cantidad de llamadas y suma de minutos de llamada; combinación de las métricas con la información de usuarios.
5. **Estadística descriptiva y visualización:** resumen de variables numéricas y distribución de planes; histogramas por plan y diagramas de caja para observar distribuciones y posibles valores atípicos.
6. **Revisión de outliers:** cálculo de límites mediante el método del rango intercuartílico (IQR) y valoración de si los valores extremos deben conservarse o tratarse.
7. **Segmentación de clientes:** creación de grupos de uso (`Bajo uso`, `Uso medio`, `Alto uso`) a partir de llamadas y mensajes, y grupos de edad (`Joven`, `Adulto`, `Adulto Mayor`); visualización de la distribución de los segmentos.
8. **Interpretación ejecutiva:** síntesis de problemas de calidad, características de los segmentos y posibles recomendaciones comerciales.

## 4. Herramientas y requisitos

- Python 3
- Jupyter Notebook o Google Colab
- `pandas`
- `numpy`
- `matplotlib`
- `seaborn`

En Google Colab, estas librerías suelen estar disponibles. Si ejecutas el notebook en otro entorno, puedes instalarlas con:

```bash
pip install pandas numpy matplotlib seaborn
```

## 5. Cómo ejecutar el notebook en Google Colab

1. Descarga o guarda el archivo `.ipynb` del proyecto en tu equipo.
2. Abre [Google Colab](https://colab.research.google.com/).
3. Selecciona **Archivo → Subir notebook** y carga el archivo `.ipynb`, o abre el notebook desde GitHub si ya está publicado.
4. Obtén los tres archivos CSV requeridos: `plans.csv`, `users_latam.csv` y `usage.csv`.
5. Sube los CSV a la sesión de Colab (panel **Archivos**) o móntalos desde Google Drive.
6. Ajusta las instrucciones `pd.read_csv(...)` de la primera sección para que apunten a la ubicación real de los archivos. Por ejemplo, si subes los tres CSV a la raíz de la sesión de Colab:

   ```python
   plans = pd.read_csv('/content/plans.csv')
   users = pd.read_csv('/content/users_latam.csv')
   usage = pd.read_csv('/content/usage.csv')
   ```

7. Ejecuta las celdas en orden, desde el inicio hasta el final, usando **Entorno de ejecución → Ejecutar todas** o ejecutando cada celda secuencialmente.
8. Revisa las salidas, tablas y gráficas. Si modificas el tratamiento de valores ausentes o atípicos, vuelve a ejecutar las celdas posteriores para que los resultados correspondan a los cambios.

## 6. Guía breve para reproducir el análisis

- **Preparar los insumos:** contar con el notebook y los tres CSV originales.
- **Configurar las rutas:** confirmar que cada `pd.read_csv()` apunta al archivo correcto.
- **Ejecutar en orden:** no omitir las celdas de carga, limpieza y creación de `user_profile`, porque las etapas posteriores dependen de ellas.
- **Validar la limpieza:** comprobar las cantidades de nulos, el tratamiento de edades inválidas y las fechas fuera del periodo considerado.
- **Revisar resultados:** comparar las estadísticas, histogramas, boxplots y tamaños de los segmentos generados.
- **Interpretar con cautela:** los resultados dependen de la calidad y cobertura de los datos. El notebook indica que los registros de uso disponibles se concentran entre enero y junio de 2024; no deben interpretarse como una representación de todo el año sin datos adicionales.
- **Documentar cambios:** si se modifican los criterios de limpieza o segmentación, registrar el cambio y volver a ejecutar el notebook completo.

## 7. Estructura sugerida del repositorio

```text
connectatel-analysis/
├── README.md
├── notebooks/
│   └── S7-Version-Estudiante-Project-ConnectaTel.ipynb
└── datasets/
    ├── plans.csv
    ├── users_latam.csv
    └── usage.csv
```

La estructura es una sugerencia; puedes organizar los archivos de otra manera. Si los datasets no se pueden compartir públicamente, no los subas al repositorio: explica cómo obtenerlos o solicita acceso a la fuente correspondiente. Evita publicar información personal o datos confidenciales.

## 8. Estado y alcance

El notebook contiene las etapas de exploración, limpieza, análisis descriptivo, visualización y segmentación, además de un apartado de análisis ejecutivo. Antes de presentar el proyecto como una entrega final, conviene verificar que todas las celdas se ejecuten de principio a fin, completar las interpretaciones que quedaron como notas o preguntas y confirmar que los nombres de las columnas utilizados en el texto coincidan con los generados por el código.

## 9. Publicación en GitHub

1. Crea un repositorio en GitHub.
2. Sube el notebook y este `README.md`; agrega los datasets únicamente si tienes permiso para compartirlos.
3. Comprueba que el README aparezca en la página principal del repositorio.
4. Abre el notebook desde GitHub o Colab y verifica que las instrucciones para acceder a los CSV sean suficientes para otra persona.
5. Usa un mensaje de commit descriptivo, por ejemplo: `docs: add ConnectaTel project README`.

---

**Nota de reproducibilidad:** el notebook original carga los datos desde `/datasets/`. Esta ruta puede no existir en Colab ni en un equipo personal; es necesario adaptar las rutas antes de ejecutar el proyecto.
