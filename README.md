# ConnectaTel — Análisis de Uso, Outliers y Segmentación de Clientes

## 🎯 Objetivo del proyecto
El objetivo de este proyecto es **analizar el comportamiento de uso de los clientes de ConnectaTel** (mensajes, llamadas y minutos de llamadas) para:
- Identificar **patrones de consumo** y **usuarios de uso extremo (outliers)**.
- Construir **segmentos de clientes** por nivel de uso y por edad.
- Generar un **insight ejecutivo** con recomendaciones para **mejorar o crear planes** basados en evidencia.

---

## 📦 Datasets utilizados
El proyecto utiliza dos datasets principales:

1. **`users` (perfil de usuario)**
   - Contiene información demográfica y de identificación del cliente.
   - Columnas típicas: `user_id`, `age` (y otras variables de usuario si aplican).

2. **`usage` / `calls` / `messages` (eventos de uso)**
   - Contiene registros transaccionales de uso (mensajes enviados, llamadas realizadas y duración).
   - A partir de estos registros se construye una tabla agregada por usuario (`usage_agg`):
     - `cant_mensajes`: cantidad total de mensajes por usuario
     - `cant_llamadas`: cantidad total de llamadas por usuario
     - `cant_minutos_llamada`: total de minutos de llamadas por usuario

> Nota: En el notebook se trabaja sobre una tabla agregada (`usage_agg`) para facilitar análisis estadístico y segmentación.

---

## 🧪 Etapas del análisis realizadas
El notebook desarrolla el flujo completo de análisis:

1. **Carga y exploración inicial**
   - Revisión de columnas, tipos de datos, valores nulos y estadísticos descriptivos.

2. **Preparación y agregación**
   - Agregación por `user_id` para obtener métricas de uso (`cant_mensajes`, `cant_llamadas`, `cant_minutos_llamada`).

3. **Integración de datasets (merge)**
   - Unión de `users` con `usage_agg` para crear `user_profile`.
   - Validación del match por `user_id` para evitar valores NaN masivos en métricas de uso.

4. **Identificación de outliers**
   - Visualización con boxplots.
   - Cálculo de límites con método **IQR** y conteo de outliers por variable.

5. **Segmentación de clientes**
   - Segmentación por **nivel de uso** (`grupo_uso`):
     - Bajo uso: llamadas < 5 y mensajes < 5
     - Uso medio: llamadas < 10 y mensajes < 10
     - Alto uso: resto
   - Segmentación por **edad** (`grupo_edad`):
     - Joven: age < 30
     - Adulto: age < 60
     - Adulto Mayor: resto

6. **Visualización de segmentos**
   - Gráficos de conteo para `grupo_uso` y `grupo_edad`.

7. **Insight ejecutivo**
   - Conclusiones accionables para stakeholders:
     - Segmentos más valiosos
     - Implicaciones de uso extremo
     - Recomendaciones de planes y ofertas

---

## ▶️ Cómo ejecutar el notebook (Google Colab)
### Opción recomendada: Google Colab
1. Sube el archivo `.ipynb` a tu Google Drive o descárgalo localmente.
2. Abre Google Colab:
   - Ve a: https://colab.research.google.com/
3. Selecciona:
   - **File → Open notebook**
4. En la pestaña:
   - **Upload** (si lo tienes local) o **Google Drive** (si está en tu Drive)
5. Ejecuta las celdas en orden:
   - **Runtime → Run all** (o ir ejecutando de arriba hacia abajo)

> Si el notebook requiere datasets externos, súbelos a Colab en la sección **Files** (panel izquierdo) o móntalos desde Google Drive.

---

## 🔁 Guía breve de reproducción (paso a paso)
Para reproducir el análisis correctamente:

1. **Cargar datasets**
   - Asegúrate de tener disponibles los archivos de usuarios y uso (según el notebook).

2. **Ejecutar limpieza y agregación**
   - Corre las celdas de preparación para construir `usage_agg`.

3. **Verificar unión de datos**
   - Al crear `user_profile`, verifica que el porcentaje de match entre IDs sea alto.
   - Indicador clave: que `cant_mensajes`, `cant_llamadas`, `cant_minutos_llamada` no queden con NaN masivo.

4. **Generar análisis de outliers**
   - Ejecuta boxplots e IQR.
   - Revisa cuántos outliers hay por variable.

5. **Crear segmentos**
   - Corre las celdas que crean `grupo_uso` y `grupo_edad`.

6. **Visualizar resultados**
   - Genera los gráficos de distribución por segmento.

7. **Leer el insight ejecutivo**
   - Interpreta hallazgos y revisa recomendaciones para planes comerciales.

---

## ✅ Resultados esperados
Al finalizar el notebook deberías tener:
- `user_profile` con métricas de uso completas.
- Tabla de límites IQR y conteo de outliers.
- Segmentación por uso y por edad.
- Visualizaciones de distribución de segmentos.
- Conclusiones ejecutivas con recomendaciones comerciales.

---

## 🧠 Notas técnicas
- Outliers se identifican con método **IQR (1.5×IQR)**.
- En modelado (si aplica), se sugiere tratar outliers con:
  - winsorización/capping o
  - transformación logarítmica (según el caso),
  sin eliminarlos del análisis de negocio, ya que pueden representar *power users*.

---

## 👤 Autor / Rol
Análisis realizado con enfoque de **Data Analyst** orientado a insights accionables para negocio (segmentación y oportunidades comerciales).