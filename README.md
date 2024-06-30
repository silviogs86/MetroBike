# MetroBike
Trabajo Final EDVai - Data Analyst BootCamp - Junio 2024.

## Table of Contents

- [Fuentes de Datos](#fuentes-de-datos)
- [Plan de Métricas](#plan-de-métricas)
- [Hipótesis](#hipótesis)
- [EDA](#eda)
- [Modelo de Datos](#modelo-de-datos)
- [Transformación y Carga de datos](#transformación-y-carga-de-datos)
  - [DataFlow](#dataflow)
  - [BigQuery](#bigquery)
  - [PowerBi](#powerbi)
- [Desarrollo dashboards](#Desarrollo-dashboards)
- [Comprobación de Hipótesis](#comprobación-de-hipótesis)
- [Links](#Links)



## Fuentes de Datos

<b>Bigquery</b>
Se utilizó el Public Dataset austin_bikeshare de los datasets publicos de BigQuery
El dataset consiste de dos tablas:

bikeshare_stations
![alt text](https://github.com/silviogs86/MetroBike/blob/4ee25795f1318c61d51307bc89ca911d865d3721/Pictures/Bronze%20Bike%20Stations.png)

bikeshare_trips
![alt text](https://github.com/silviogs86/MetroBike/blob/4ee25795f1318c61d51307bc89ca911d865d3721/Pictures/Bronze%20bike%20trips.png)

<b>Página Web</b>
Utilizaremos la página de MetroBike: https://austin.bcycle.com/passes

## Plan de Métricas
El Plan de metricas es el siguiente:
![alt text](https://github.com/silviogs86/MetroBike/blob/88fae7a832c76871894e4914f7971fa7fdea4d3e/Pictures/PlanMetricas.png)



## Hipótesis 

<b>Hipótesis 1:</b>
Se utilizan más bicicletas eléctricas que comunes.

<b>Hipótesis 2:</b>
En primavera y verano hay más demanda de uso de bicicletas.

<b>Hipótesis 3:</b>
Los planes cortos (explorer y 3day) tienen menos surplus que los 30 y 365.

<b>Hipótesis 4:</b>
Los planes universitarios tienen un uso marginal dentro de la plataforma.

## EDA 
En el EDA, detectamos lo siguiente:

*Hay stations duplicadas en la tabla trips con distintos caracteres vs la tabla stations
![alt text](https://github.com/silviogs86/MetroBike/blob/26c0f024fd26ee965ea458fcff16b93687205fc2/Pictures/BigQuery/Stations%20EDA.png)

<b>1st comparison</b>

![alt text](https://github.com/silviogs86/MetroBike/blob/26c0f024fd26ee965ea458fcff16b93687205fc2/Pictures/BigQuery/Stations%20EDA%20Results.png)
![alt text](https://github.com/silviogs86/MetroBike/blob/26c0f024fd26ee965ea458fcff16b93687205fc2/Pictures/BigQuery/Trips%20EDA%20Results.png)

<b>2nd comparison</b>

![alt text](https://github.com/silviogs86/MetroBike/blob/b03fbabcd8faf9e8298b98d9d17fb50d56794b20/Pictures/BigQuery/Trips%20EDA%20Results%202.png)![alt text](https://github.com/silviogs86/MetroBike/blob/b03fbabcd8faf9e8298b98d9d17fb50d56794b20/Pictures/BigQuery/Stations%20EDA%20Results2.png)

*En la tabla trips en las columnas de start y end station hay ids null y hay ids distintos para un mismo name.

<b>Start Stations</b>

![alt text](https://github.com/silviogs86/MetroBike/blob/a7fe356370e02588df901bf643cf738b5650ec0d/Pictures/BigQuery/Trips%20EDA%20IDs.png)

![alt text](https://github.com/silviogs86/MetroBike/blob/a7fe356370e02588df901bf643cf738b5650ec0d/Pictures/BigQuery/Trips%20ID%20EDA%20Results.png)

![alt text](https://github.com/silviogs86/MetroBike/blob/a7fe356370e02588df901bf643cf738b5650ec0d/Pictures/BigQuery/Trips%20ID%20EDA%20Results2.png)

![alt text](https://github.com/silviogs86/MetroBike/blob/a7fe356370e02588df901bf643cf738b5650ec0d/Pictures/BigQuery/Trips%20ID%20EDA%20Results3.png)

<b>End Stations</b>

![alt text](https://github.com/silviogs86/MetroBike/blob/a7fe356370e02588df901bf643cf738b5650ec0d/Pictures/BigQuery/Trips%20EDA%202%20IDs.png)

![alt text](https://github.com/silviogs86/MetroBike/blob/a7fe356370e02588df901bf643cf738b5650ec0d/Pictures/BigQuery/Trips2%20IDs%20results.png)

![alt text](https://github.com/silviogs86/MetroBike/blob/a7fe356370e02588df901bf643cf738b5650ec0d/Pictures/BigQuery/Trips2%20IDs%20results2.png)

*En la tabla trips aparecen subscribers que no estan vigentes en el cuadro tarifario actual y no se visualiza un subscriber ID.<br>
![alt text](https://github.com/silviogs86/MetroBike/blob/6a0ffd29481e009b31aeb1939c7b01b1c2862abf/Pictures/BigQuery/Subscribers%20EDA.png)<br>
![alt text](https://github.com/silviogs86/MetroBike/blob/b03fbabcd8faf9e8298b98d9d17fb50d56794b20/Pictures/BigQuery/Subscribers%20EDA%20Results.png)

## Modelo de Datos
Como no tenemos analisis que realizar sobre las stations y la información provista no está completa, dejamos las columnas fuera del silver.

Las tablas que vamos a necesitar serían:<br>
DIM_Bike_Types<br>
DIM_Subscriber_Types<br>
FACT_Trips


![alt text](https://github.com/silviogs86/MetroBike/blob/42cb5575b212552d03a77701bc0532265ae6f9f7/Pictures/Austin-Bikes.png)

## Transformación y Carga de datos 

### DataFlow 
El flujo de datos queda definido de la siguiente manera
![alt text](https://github.com/silviogs86/MetroBike/blob/42cb5575b212552d03a77701bc0532265ae6f9f7/Pictures/Opciones%20de%20flujo.jpg)


### BigQuery 

Las queries serían

DIM_Bike_Types<br>
![alt text](https://github.com/silviogs86/MetroBike/blob/4ee25795f1318c61d51307bc89ca911d865d3721/Pictures/Query%20For%20Bike%20Types%20Table.png)

DIM_Subscriber_Types<br>
![alt text](https://github.com/silviogs86/MetroBike/blob/9402e965918e61647c4f01eff9ad830b8983680a/Pictures/Subscriber%20Type%20Query%20Pt.1.png)

y luego<br>
![alt text](https://github.com/silviogs86/MetroBike/blob/42cb5575b212552d03a77701bc0532265ae6f9f7/Pictures/Subscriber%20Type%20Query%20Pt.2.png)

FACT_Trips<br>
![alt text](https://github.com/silviogs86/MetroBike/blob/4ee25795f1318c61d51307bc89ca911d865d3721/Pictures/Query%20For%20Trips%20Table.png)


### PowerBi 

Luego subimos la información a Power BI

Las tablas de BigQuery
![alt text](https://github.com/silviogs86/MetroBike/blob/463124e913d7a2bf4a7858ece4803471f97a01aa/Pictures/BQ%20to%20PowerBI.png)

La tabla de montos de los pases de la web https://austin.bcycle.com/passes
![alt text](https://github.com/silviogs86/MetroBike/blob/463124e913d7a2bf4a7858ece4803471f97a01aa/Pictures/Web%20to%20PowerBi%20pt1.png)

y luego

![alt text](https://github.com/silviogs86/MetroBike/blob/463124e913d7a2bf4a7858ece4803471f97a01aa/Pictures/Web%20to%20PowerBi%20pt2.png)

Dentro de power BI realizamos las siguientes transformaciones:

<b>Power Query</b>

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

7 Crear una tabla de horas<br>
![alt text](https://github.com/silviogs86/MetroBike/blob/e9c38720cab71030b68a2634dabdd30914b18dd2/Pictures/PowerBi/Dax%207.png)

8 Agregar a tabla FACT_Trips las columnas FactDate, TripHour y SurplusFee
![alt text](https://github.com/silviogs86/MetroBike/blob/3397867687742203da239e114d83f19f516036c0/Pictures/PowerBi/Dax%208a.png)

![alt text](https://github.com/silviogs86/MetroBike/blob/3397867687742203da239e114d83f19f516036c0/Pictures/PowerBi/Dax%208b.png)

![alt text](https://github.com/silviogs86/MetroBike/blob/3397867687742203da239e114d83f19f516036c0/Pictures/PowerBi/Dax%208c.png)

Estructura final de PowerBi
![alt text](https://github.com/silviogs86/MetroBike/blob/3397867687742203da239e114d83f19f516036c0/Pictures/PowerBi/Estructura%20PBI.png)

## Desarrollo dashboards

El desarrollo de los dashboards se realizó de la siguiente manera:<br>

Portada: Modificamos el fondo del canva utilizando el color oficial de la web de Metrobike. y pusimos los tres iconos que llevan cada uno a su respectiva página<br>
![alt text](https://github.com/silviogs86/MetroBike/blob/27a1f6f53d1268153b336eeba78296adf92332f6/Pictures/PowerBi/Dashboard/Cover.png)

<b>Usage:</b> El objetivo de este dashboard es brindar respuestas a las metricas #1 (Viajes por plan) y #2 (Estacionalidad) de ventas y #1 (Tipo de bicicletas) de Operaciones<br>
En primer lugar setee los filtros de información:<br>
2 Treemap<br>
Tipo de Bicicleta<br>
Estación del año<br>
4 filtros<br>
Tipo de Plan<br>
Año<br>
Mes<br>
Feriado<br>

En segundo lugar setee las visualizaciones, decidí poner lo siguiente:<br>
2 Cards<br>
2 Bar Chart<br>
1 Pie Chart<br>

En los cards mostrar el total de los viajes y el total del año pasado para poder ver tendencia:<br>

En los bar chart las cantidades de viajes por hora y por Mes-Año (elegi poner como mes-año y no solo mes para que se vea a simple vista del grafico en que año se esta observando)<br>

En el pie chart las distribución del total de viajes en 3 grandes categorías:<br>
Menos de 60 minutos<br>
Más de 60 minutos y menos de 24 horas<br>
Más de 24 horas<br>

![alt text](https://github.com/silviogs86/MetroBike/blob/27a1f6f53d1268153b336eeba78296adf92332f6/Pictures/PowerBi/Dashboard/Usage.png)<br>
![alt text](https://github.com/silviogs86/MetroBike/blob/27a1f6f53d1268153b336eeba78296adf92332f6/Pictures/PowerBi/Dashboard/Usage%20Filters.png)<br>
![alt text](https://github.com/silviogs86/MetroBike/blob/27a1f6f53d1268153b336eeba78296adf92332f6/Pictures/PowerBi/Dashboard/Usage%20charts%201.png)<br>
![alt text](https://github.com/silviogs86/MetroBike/blob/27a1f6f53d1268153b336eeba78296adf92332f6/Pictures/PowerBi/Dashboard/Usage%20charts%202.png)<br>

<b>Regular plans & college</b><br>
Para estos dashboards utilice la misma logica, la unica diferencia es que en Regular Plans puse un filtro de página para que no cuente los planes universitarios (HT y UT) y en College para que no cuente los planes de regular (pay, 3day,explorer, local 30 y local 365.<br>.
![alt text](https://github.com/silviogs86/MetroBike/blob/27a1f6f53d1268153b336eeba78296adf92332f6/Pictures/PowerBi/Dashboard/Page%20Filter.png)<br>
El objetivo de regular plans, es dar respuesta a la metrica "Surplus por plan" y el de college a la metrica "Performance..."<br>

Los filtros fueron reutilizados de Usage:<br>
2 treemap<br>
3 filtros<br>
Las visuales elegidas son:<br>
2 pie chart<br>
2 clustered bar chart (horizontal)<br>
1 card<br>

La card con el total para que al ver distintos valores no sea necesario hacer la cuenta, siempre va a mostrar el total de los valores seleccionados.<br>
Los pie chart los utilicé para graficar los totales de cantidad de viajes y monto generado en surplus. Decidí utilizar el grafico de barras horizontal para los promedios porque me parece que confunde visualmente poner el mismo grafico para todo.

![alt text](https://github.com/silviogs86/MetroBike/blob/27a1f6f53d1268153b336eeba78296adf92332f6/Pictures/PowerBi/Dashboard/Plans%20%26%20college.png)<br>
![alt text](https://github.com/silviogs86/MetroBike/blob/27a1f6f53d1268153b336eeba78296adf92332f6/Pictures/PowerBi/Dashboard/Plans%20%26%20college%20charts%201.png)<br>
![alt text](https://github.com/silviogs86/MetroBike/blob/27a1f6f53d1268153b336eeba78296adf92332f6/Pictures/PowerBi/Dashboard/Plans%20%26%20college%20charts%202.png)<br>

<b>Navegación reporte</b>
Para la navegación del reporte utilizamos los 3 iconos de la portada y el logotipo de metrobike.<br>
![alt text](https://github.com/silviogs86/MetroBike/blob/dcd275fbd2b6aff80d8e7e5896df495c27cfea68/Pictures/PowerBi/Dashboard/Navigation.png)<br>
El logotipo actúa como home, los iconos para navegar dentro del reporte, para marcar que estamos en una página determinada dejamos el icono correspondiente con fondo blanco



## Comprobación de Hipótesis
<b>Hipótesis 1:</b>
Se utilizan más bicicletas eléctricas que comunes.

<b>Resultado</b>
De la totalidad de viajes, el 67% se realizó con biciletas comunes, pero a partir de 2020 la cantidad de usos de bicicleta electrica ha subido, en detrimento de la bicicleta clasica. En conclusión historicamente se han utilizado más clasicas, pero de 2020 a el día de hoy, el uso de bicileta electrica va en aumento

<b>Hipótesis 2:</b>
En primavera y verano hay más demanda de uso de bicicletas.

<b>Resultado</b>
Viendo el historico de viajes en la hoja "Usage" comprobamos que se usan más bicicletas en primavera y otoño, ocupando el verano un 3er lugar por una diferencia de 47 mil viajes.

<b>Hipótesis 3:</b>
Los planes cortos (explorer y 3day) tienen menos surplus que los 30 y 365.

<b>Resultado</b>
Al contrario de lo que uno podría creer los planes de menor duración tienen más surplus. Explorer y 3Day tienen un 45% de los viajes surplus. El 75% del surplus de los planes tradicionales, está concentrado en los planes de corta duración (pay as you ride, explorer y 3day)

<b>Hipótesis 4:</b>
Los planes universitarios tienen un uso marginal dentro de la plataforma.

<b>Resultado</b>
El Plan sin cargo (HT) tiene un uso minimo, pero el plan de $12 al año (U.T.) es:
- el segundo plan con mayor cantidad de viajes detras de Local365.
- el tercer plan en cantidad de viajes surplus.


## Links
[Link al plan de metricas](https://docs.google.com/spreadsheets/d/1w6sxddYLm-WwrIuhsbntgmVx5Utpo9LNyN_dhmUGgV8/edit?gid=906195733#gid=906195733)

[Link al pbix](https://1drv.ms/f/s!AkfPVJizTvY_hkV4DP0tGVoy52PB?e=cSRGK5)

[Link al reporte](https://app.powerbi.com/view?r=eyJrIjoiOWEwZTc1YTYtMGU4MC00YjlkLWIzNWMtMzE2YWNlZThhMTlmIiwidCI6IjNmN2FlM2QzLTYyN2ItNDJmMS1hMjU5LTE5ZmMyMGM4MGZlYSIsImMiOjR9&pageName=ReportSection01ecdbea88e19d749646)
