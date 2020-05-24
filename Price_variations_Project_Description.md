## Price Intelligence with Python and Pandas

<p style="font-size:13px">Click <a href="https://github.com/andjimbon/Mercadolibre-Tucarro-Project/blob/master/script-publication-series.ipynb">Here</a> to see Code</p>

**Project description:** With this project you will be able to track Mercadolibre daily publications and identify variations in the price of products.

Note:

The script assumes that there are two files (Table1, Table2) containing scraped data from the two previous days (n-1, n-2)


### 1.  Merge Tables

To calculate variations in the price of the product, it's necessary to merge the previous crawled tables and create new fields

```python
# Merge
    table2_mod = pd.merge(table1, table2, on=['a_id'], how='right', suffixes=('_old', '_new'))
```

```python
    # Accumulated columns
    table2_mod['delta_precio'] = table2_mod['Precio'] - table2_mod['g_precio_old'] # Calculation
    table2_mod['delta_precio'].fillna(0, inplace=True) # Replace NAN with 0
    table2_mod['pct_delta_precio'] = table2_mod['Precio']/table2_mod['g_precio_old'] -1 # Calculation
    table2_mod['pct_delta_precio'].fillna(0, inplace=True) # # Replace NAN with 0
    table2_mod['flg_delta_precio'] = np.where(table2_mod['delta_precio'] != 0, 1,0) # Calculation
    table2_mod['Fecha_ini_monitor'] = table2_mod['r_fecha_info_old'].combine_first(table2_mod['Fecha_scraping']) # Calculation
    table2_mod['Ctd_dias_monitor'] = table2_mod['Fecha_scraping'] - table2_mod['Fecha_ini_monitor'] # Calculation
    table2_mod['Ctd_dias_monitor'] = table2_mod['Ctd_dias_monitor'] / np.timedelta64(1, 'D') # Remove 'days' word from results
    table2_mod['Ctd_dias_monitor'].fillna(0, inplace=True)
    table2_mod['Ctd_dias_monitor'] = table2_mod['Ctd_dias_monitor'].round()
    table2_mod['precio_inicial'] = table2_mod['g_precio_old'].combine_first(table2_mod['Precio']) # Calculation

    # Equivalents
    table2_mod['Acum_delta'] = table2_mod['delta_precio']
    table2_mod['Acum_pct_delta'] = table2_mod['pct_delta_precio']
    table2_mod['cambios_totales'] = table2_mod['flg_delta_precio']

    # NaN column for first join
    table2_mod['fecha_ult_mod'] = np.datetime64()
```

### 2. Conditional executing Function 

The script will run the function "first_join" if we haven't merging any table before. 

### 3. Final Table

[Click Here ](https://www.dropbox.com/s/votc015fn0ajr1m/Base_datos_actualizaciones_ejemplo.xlsx?dl=0) to view an example that shows the changes in the prices of different products over a period of time.

<img src="images/price_var.PNG?raw=true"/>

