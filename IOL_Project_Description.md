## Real-Time Argentinian Bond Price

<p style="font-size:13px">Click <a href="https://github.com/andjimbon/Invertiroline-prices-real-time/blob/master/Chart%20bond%20prices%20-%20Invertironline.ipynb">Here </a>to see Code</p>

**Project description:** Get real-time bond prices from a live chart and put data into a structured pandas table. 

This code allows you to do analysis in real-time for bonds, stocks or other financial instruments whitout an API

To get live data from [InvertirOnline](https://www.invertironline.com/) you must have an active account.


### 1. Gettin' Data

The web page uses the POST REQUEST method to construct the live chart, so we need to get some information in the "Inspect-Network" tool

```javascript
url = 'https://www.invertironline.com/titulo/cotizacion/BCBA/AY24/BONOS-NACION-ARGENTINA-USD-8.75--2024'

headers={
    'Referer': 'https://www.invertirhttps://www.invertironline.com/titulo/cotizacion/BCBA/AY24/BONOS-NACION-ARGENTINA-USD-8.75--2024/graficador',
    'Cookie': '_ga=GA1.2.1419134137.1529598737; i18n.langtag=es-AR; utm_path=ID_origen=99&utm_source=Newsletter&utm_medium=email&utm_campaign=NL_IOL_Research_AperturaDeMercado_CA_30-Jul-19&embtrk=7i7,-R-21368403-R-,a8bi-R-ac7,n9; isMobile=0; _hjid=5d2124d6-1d1f-4432-b663-01fdcfc5448e; _gcl_au=1.1.1127974570.1569418667; _fbp=fb.1.1569520643782.1145300030; uid=631261; _gid=GA1.2.904748864.1570629820; __sidglobal=libjy2todwnixmpbhcrwxjsz; isLogged=1; _dc_gtm_UA-189938-1=1',
    'X-Requested-With': 'XMLHttpRequest',
    'Accept': 'application/json, text/javascript, */*; q=0.01',
    'Accept-Encoding': 'gzip, deflate, br',
    'Accept-Language': 'en,es;q=0.9,pt;q=0.8',
    'Connection': 'keep-alive',
    'Host': 'www.invertironline.com',
    'User-Agent': 'Mozilla/5.0 (Linux; Android 6.0; Nexus 5 Build/MRA58N) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/77.0.3865.90 Mobile Safari/537.36'
}
```

### 2. Loadin' Content with BeautifulSoup

```javascript
 r = requests.post(url, headers=headers)
r_ = BeautifulSoup(r.content,'html.parser')
```

Iterate over live data to create a table using **list comprehension:**

```python
# TABLE HEADERS
table_header = r_.find('table', id='tablaOpsIntrad').find('thead')

t_headers=[]
for tr in table_header.find_all('tr'):
    row_headers = [td.text for td in tr.find_all('td')]
    t_headers.append(row_headers)
    
t_headers=t_headers[1:][0] #List of lists. Taking the first item

# TABLA INTRADIARIA
table = r_.find('table', id='tablaOpsIntrad').find('tbody')

data=[]
for tr in table.find_all('tr'):
    row_text = [td.text for td in tr.find_all('td')]
    data.append(row_text)
```

### 3. Convertin' data to a Pandas Dataframe

| Hour | Precio | Volumen
------------ | ------------- | -------------
16:54 | 2425.0 | 14403
16:54 | 2424.0| 300
16:55 | 2422.0| 1000
