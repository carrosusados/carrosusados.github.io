## Real Estate Market in Colombia

<p style="font-size:13px">Click <a href="https://github.com/andjimbon/Mercadolibre-Property-Scrapy-Project/blob/master/Meli%20Property/property_meli.py">Here</a> to see Code</p>

**Project description:** With this code you will be abble to compare market prices for sellig or renting properties (Apartments/Houses/Offices) from diferent neighboorhoods or cities in Colombia, and get the information from each property publication (Rooms, bathrooms, M2, House Expenses, etc.)

This algorithm scrapes data from [Mercadolibre Colombia](https://www.mercadolibre.com.co/inmuebles) and creates a database with property items and their Google geogrpahical location.


### 1. Define locations

Enter the link locations inside the "start_request" function by filtering in the web page 

```javascript
def start_requests(self):
        yield scrapy.Request(
            'https://listado.mercadolibre.com.co/inmuebles/apartamentos/venta/bogota-dc/suba/acacias/_DisplayType_LF',
            self.parse)
```

### 2. Run Spider

Run the script and automatically the file will be save in the folder where the script is. Modify the file's name in the "custom_settings":

```javascript
 custom_settings = {
        'FEED_URI': 'inmuebles_' + str(datetime.today().strftime('%Y-%m-%d')) + '.csv',
        'FEED_FORMAT': 'csv',
        'FEED_EXPORTERS': {
            'json': 'scrapy.exporters.CsvItemExporter',
        }
```
Once finished the process, you'll receive and email with the stats:

Global Stats | 
------------ | -------------
start_time | 2020-01-05 23:44:09.213644
item_scraped_count | 329311
elapsed_time_seconds | 3853.932806
finish_time | 2020-01-06 10:28:23.146450
finish_reason | finished


### 3. Final Table

[Click Here ](https://www.dropbox.com/s/83q7mc0n3eodb1n/Base_Datos_ejemplo.xlsx?dl=0)to view an example that shows the structured data

<img src="images/Table.PNG?raw=true"/>

