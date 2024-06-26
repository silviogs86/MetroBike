# MetroBike
Trabajo Final EDVai - Data Analyst BootCamp - Junio 2024.

Se utilizó el Public Dataset austin_bikeshare de los datasets publicos de BigQuery
El dataset consiste de dos tablas:

bikeshare_stations
![alt text](https://github.com/silviogs86/MetroBike/blob/4ee25795f1318c61d51307bc89ca911d865d3721/Pictures/Bronze%20Bike%20Stations.png)

bikeshare_trips
![alt text](https://github.com/silviogs86/MetroBike/blob/4ee25795f1318c61d51307bc89ca911d865d3721/Pictures/Bronze%20bike%20trips.png)

El Plan de metricas es el siguiente:
![alt text](https://github.com/silviogs86/MetroBike/blob/aab5839099565b4093da3bcc2f246618ed88e12e/Pictures/Plan%20De%20Metricas.png)


En el EDA, detectamos lo siguiente:

*Hay stations duplicadas en la tabla stations (las duplicadas estan inactive)

*En la tabla trips en las columnas de start y end station hay ids null y hay ids distintos para un mismo station name.

*En la tabla trips aparecen subscribers que no estan vigentes en el cuadro tarifario actual y no se visualiza un subscriber ID.


Como no tenemos analisis que realizar sobre las stations y la información provista no está completa, dejamos las columnas fuera del silver.

Las tablas que vamos a necesitar serían:
FACT_Trips
DIM_Bike_Types
DIM_Subscriber_Types

Las queries serían

DIM_Bike_Types

![alt text](https://github.com/silviogs86/MetroBike/blob/4ee25795f1318c61d51307bc89ca911d865d3721/Pictures/Query%20For%20Bike%20Types%20Table.png)

DIM_Subscriber_Types

![alt text](https://github.com/silviogs86/MetroBike/blob/9402e965918e61647c4f01eff9ad830b8983680a/Pictures/Subscriber%20Type%20Query%20Pt.1.png)

y luego

![alt text](https://github.com/silviogs86/MetroBike/blob/42cb5575b212552d03a77701bc0532265ae6f9f7/Pictures/Subscriber%20Type%20Query%20Pt.2.png)

FACT_Trips

![alt text](https://github.com/silviogs86/MetroBike/blob/4ee25795f1318c61d51307bc89ca911d865d3721/Pictures/Query%20For%20Trips%20Table.png)

La relación entre tablas sería la siguiente
![alt text](https://github.com/silviogs86/MetroBike/blob/42cb5575b212552d03a77701bc0532265ae6f9f7/Pictures/Austin-Bikes.png)

El flujo de datos queda definido de la siguiente manera
![alt text](https://github.com/silviogs86/MetroBike/blob/42cb5575b212552d03a77701bc0532265ae6f9f7/Pictures/Opciones%20de%20flujo.jpg)

Luego subimos la información a Power BI

Las tablas de BigQuery
![alt text](https://github.com/silviogs86/MetroBike/blob/463124e913d7a2bf4a7858ece4803471f97a01aa/Pictures/BQ%20to%20PowerBI.png)

La tabla de montos de los pases de la web https://austin.bcycle.com/passes
![alt text](https://github.com/silviogs86/MetroBike/blob/463124e913d7a2bf4a7858ece4803471f97a01aa/Pictures/Web%20to%20PowerBi%20pt1.png)

y luego
![alt text](https://github.com/silviogs86/MetroBike/blob/463124e913d7a2bf4a7858ece4803471f97a01aa/Pictures/Web%20to%20PowerBi%20pt2.png)

Dentro de power BI realizamos las siguientes transformaciones:

Power Query
1 En la Tabla AB_PassPrices poner "|" entre el plan name y la descripción y los montos
![alt text](https://github.com/silviogs86/MetroBike/blob/3397867687742203da239e114d83f19f516036c0/Pictures/PowerBi/PowerQuery%201.png)

2 Cargar a mano los valores de los planes universitarios fuera del link de prices (la información fue obtenida de los siguientes links:
https://austin.bcycle.com/university-of-texas-at-austin
https://austin.bcycle.com/houston-tillotson-university
![alt text](https://github.com/silviogs86/MetroBike/blob/3397867687742203da239e114d83f19f516036c0/Pictures/PowerBi/PowerQuery%202.png)


3 Append queries en una tabla nueva
![alt text](https://github.com/silviogs86/MetroBike/blob/3397867687742203da239e114d83f19f516036c0/Pictures/PowerBi/PowerQuery%203.png)

4 Separar por delimeter utilizando el "|" que pusimos anteriormente. El resultado final
![alt text](https://github.com/silviogs86/MetroBike/blob/3397867687742203da239e114d83f19f516036c0/Pictures/PowerBi/PowerQuery%204.png)

5 Mergear tabla con tabla DIM_Subscriber_Types para tener junto al ID los montos de plan y surplus
![alt text](https://github.com/silviogs86/MetroBike/blob/3397867687742203da239e114d83f19f516036c0/Pictures/PowerBi/PowerQuery%205.png)

<b>Dax</b>
6 Crear una tabla calendario
![alt text](https://github.com/silviogs86/MetroBike/blob/3397867687742203da239e114d83f19f516036c0/Pictures/PowerBi/Dax%206.png)

7 Crear una tabla de horas
![alt text](https://gitshub.com/silviogs86/MetroBike/blob/3397867687742203da239e114d83f19f516036c0/Pictures/PowerBi/Dax%207.png)

8 Agregar a tabla FACT_Trips las columnas FactDate, TripHour y SurplusFee
![alt text](https://github.com/silviogs86/MetroBike/blob/3397867687742203da239e114d83f19f516036c0/Pictures/PowerBi/Dax%208a.png)

![alt text](https://github.com/silviogs86/MetroBike/blob/3397867687742203da239e114d83f19f516036c0/Pictures/PowerBi/Dax%208b.png)

![alt text](https://github.com/silviogs86/MetroBike/blob/3397867687742203da239e114d83f19f516036c0/Pictures/PowerBi/Dax%208c.png)

Estructura final de PowerBi
![alt text](https://github.com/silviogs86/MetroBike/blob/3397867687742203da239e114d83f19f516036c0/Pictures/PowerBi/Estructura%20PBI.png)


