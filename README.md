# 📊 Circular Line Chart
This project contains a circular line chart comparing the project baseline with monthly finishes. It uses Python libraries including pandas, numpy, and matplotlib to generate a visually appealing and easy-to-interpret chart.

## 🚀 Description
The circular line chart visualizes project evolution over time, clearly showing differences between planned and actual activity completion dates.

## 📑 Notebook Contents
The `Circular Line Chart.ipynb` file includes:

1. **Library Imports** 📦
   ```python
   import pandas as pd
   import numpy as np
   import matplotlib.pyplot as plt
   ```
2. **Excel File Reading** 📥
   ```python
   df = pd.read_excel('GPT - Circular Line Chart.xlsx')
   ```
3. **Date Column Conversion** 📅
   ```python
   date_columns = ['Project Baseline Finish', 'M-1 Finish', 'M-2 Finish', 'M-3 Finish', 'Current Finish']
   for col in date_columns:
       df[col] = pd.to_datetime(df[col])
   ```
4. **DataFrame Sorting** 📊
   ```python
   df = df.sort_values('Project Baseline Finish').reset_index(drop=True)
   ```
5. **Date Normalization to Radial Scale** 🌀
   ```python
   def normalize_dates(dates, start_date):
       return [(date - start_date).days / 365.25 for date in dates]
   ```
6. **Chart Setup and Creation** 🎨
   ```python
   plt.figure(figsize=(12, 12), dpi=100)
   ax = plt.subplot(111, polar=True)
   ax.set_theta_offset(np.pi / 2)
   ax.set_theta_direction(-1)
   ```
7. **Adding Year Rings and Labels** 🔄
   ```python
   for year in range(2023, 2030):
       ring_radius = year - 2023
       ax.plot(np.linspace(0, 2 * np.pi, 100), [ring_radius] * 100, linestyle='--', color='grey', linewidth=1, alpha=0.6)
       if ring_radius >= 0:
           ax.text(0, ring_radius, str(year), ha='center', va='bottom', fontsize=10, color='black')
   ```
8. **Adding Today's Circle** 📅
   ```python
   today = pd.Timestamp('today').normalize()
   today_radial = normalize_dates([today], start_date)[0]
   ax.plot(np.linspace(0, 2 * np.pi, 500), [today_radial]*len(theta), linestyle='--', color='red', linewidth=1, label='Today')
   ```
9. **Adding Legend and Title** 🏷️
   ```python
   plt.legend(loc='lower right', fontsize=10)
   plt.title('Circular Line Chart: Project Baseline vs Monthly Finishes', va='bottom')
   ```
10. **Saving and Displaying Chart** 💾
    ```python
    plt.savefig('Circular_Line_Chart.png', format='png', transparent=True)
    plt.show()
    ```

## 🛠️ Requirements
Required libraries:
- pandas
- numpy
- matplotlib

Install via pip:
```sh
pip install pandas numpy matplotlib
```

## 📈 Execution
Open `Circular Line Chart.ipynb` in Jupyter Notebook or JupyterLab and run the cells.

## 📃 License
This project is under the Apache License. See LICENSE file for details.
