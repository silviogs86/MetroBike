# MetroBike
Trabajo Final EDVai - Data Analyst BootCamp - Junio 2024.

Se utilizó el Public Dataset austin_bikeshare de los datasets publicos de BigQuery
El dataset consiste de dos tablas:


bikeshare_stations
![alt text](https://github.com/silviogs86/MetroBike/blob/4ee25795f1318c61d51307bc89ca911d865d3721/Pictures/Bronze%20Bike%20Stations.png)

bikeshare_trips
![alt text](https://github.com/silviogs86/MetroBike/blob/4ee25795f1318c61d51307bc89ca911d865d3721/Pictures/Bronze%20bike%20trips.png)

En el EDA, detectamos lo siguiente:

*Hay stations duplicadas en la tabla stations (las duplicadas estan inactive)

*En la tabla trips en las columnas de start y end station hay ids null y hay ids distintos para un mismo station name.

*En la tabla trips aparecen subscribers que no estan vigentes en el cuadro tarifario actual y no se visualiza un subscriber ID.


Como no tenemos analisis que realizar sobre las stations y la información provista no está completa, dejamos las columnas fuera del silver.

Las queries serían

DIM_Bike_Types
![alt text](https://github.com/silviogs86/MetroBike/blob/4ee25795f1318c61d51307bc89ca911d865d3721/Pictures/Query%20For%20Bike%20Types%20Table.png)

DIM_Subscriber_Types
![alt text](https://github.com/silviogs86/MetroBike/blob/4ee25795f1318c61d51307bc89ca911d865d3721/Pictures/1st%20part%20of%20Subscriber%20Type%20Query.png)

y luego
![alt text](https://github.com/silviogs86/MetroBike/blob/42cb5575b212552d03a77701bc0532265ae6f9f7/Pictures/Subscriber%20Type%20Query%20Pt.2.png)

FACT_Trips
![alt text](https://github.com/silviogs86/MetroBike/blob/4ee25795f1318c61d51307bc89ca911d865d3721/Pictures/Query%20For%20Trips%20Table.png)

La relación entre tablas sería la siguiente
![alt text](https://github.com/silviogs86/MetroBike/blob/42cb5575b212552d03a77701bc0532265ae6f9f7/Pictures/Austin-Bikes.png)

El flujo de datos queda definido de la siguiente manera
![alt text](https://github.com/silviogs86/MetroBike/blob/42cb5575b212552d03a77701bc0532265ae6f9f7/Pictures/Opciones%20de%20flujo.jpg)



