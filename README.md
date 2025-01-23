# 📊 Circular Line Chart

Este proyecto contiene un gráfico de líneas circular que compara la línea base del proyecto con los finales mensuales. Utiliza Python y varias bibliotecas como pandas, numpy y matplotlib para generar un gráfico visualmente atractivo y fácil de interpretar.

## 🚀 Descripción

El gráfico de líneas circular es una herramienta útil para visualizar la evolución de un proyecto a lo largo del tiempo. Este enfoque permite ver claramente las diferencias entre las fechas planificadas y las fechas reales de finalización de las actividades.

## 📑 Contenido del Notebook

El archivo `Circular Line Chart.ipynb` incluye el siguiente contenido:

1. **Importación de Bibliotecas** 📦
   ```python
   import pandas as pd
   import numpy as np
   import matplotlib.pyplot as plt
   ```

2. **Lectura del Archivo Excel** 📥
   ```python
   df = pd.read_excel('GPT - Circular Line Chart.xlsx')
   ```

3. **Conversión de Columnas de Fechas** 📅
   ```python
   date_columns = ['Project Baseline Finish', 'M-1 Finish', 'M-2 Finish', 'M-3 Finish', 'Current Finish']
   for col in date_columns:
       df[col] = pd.to_datetime(df[col])
   ```

4. **Ordenación del DataFrame** 📊
   ```python
   df = df.sort_values('Project Baseline Finish').reset_index(drop=True)
   ```

5. **Normalización de Fechas a una Escala Radial** 🌀
   ```python
   def normalize_dates(dates, start_date):
       return [(date - start_date).days / 365.25 for date in dates]
   ```

6. **Configuración y Creación del Gráfico** 🎨
   ```python
   plt.figure(figsize=(12, 12), dpi=100)
   ax = plt.subplot(111, polar=True)
   ax.set_theta_offset(np.pi / 2)
   ax.set_theta_direction(-1)
   ```

7. **Añadir Anillos para Cada Año y Etiquetas** 🔄
   ```python
   for year in range(2023, 2030):
       ring_radius = year - 2023
       ax.plot(np.linspace(0, 2 * np.pi, 100), [ring_radius] * 100, linestyle='--', color='grey', linewidth=1, alpha=0.6)
       if ring_radius >= 0:
           ax.text(0, ring_radius, str(year), ha='center', va='bottom', fontsize=10, color='black')
   ```

8. **Añadir la Circunferencia para el Día de Hoy** 📅
   ```python
   today = pd.Timestamp('today').normalize()
   today_radial = normalize_dates([today], start_date)[0]
   ax.plot(np.linspace(0, 2 * np.pi, 500), [today_radial]*len(theta), linestyle='--', color='red', linewidth=1, label='Today')
   ```

9. **Agregar Leyenda y Título** 🏷️
   ```python
   plt.legend(loc='lower right', fontsize=10)
   plt.title('Circular Line Chart: Project Baseline vs Monthly Finishes', va='bottom')
   ```

10. **Guardar y Mostrar el Gráfico** 💾
    ```python
    plt.savefig('Circular_Line_Chart.png', format='png', transparent=True)
    plt.show()
    ```

## 🛠️ Requisitos

Para ejecutar el notebook, necesitas tener instaladas las siguientes bibliotecas:
- pandas
- numpy
- matplotlib

Puedes instalarlas usando pip:
```sh
pip install pandas numpy matplotlib
```

## 📈 Ejecución

Para ejecutar el notebook, simplemente abre `Circular Line Chart.ipynb` en Jupyter Notebook o JupyterLab y ejecuta las celdas.

## 📃 Licencia

Este proyecto está bajo la licencia MIT. Consulta el archivo LICENSE para más detalles.
