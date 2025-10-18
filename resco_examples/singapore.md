## Example: Singapore - Weather Conditions

Domain: Climate

Data source: [Singapore Real Time Weather Readings Datasets](https://data.gov.sg/collections/1459/view)

### 1. Singapore Instruments and Readings from Weather Stations

We can model weather condition data from readings in various weather stations across Singapore. Singapore has various weather readings datasets available, including data on air temperature, rainfall, relative humidity, wind direction and wind speed. For our modeling examples, we'll explore modeling air temperature and humidity data.

**Weather Stations and Thermometers as Entities**

We can model each weather station across Singapore as an Entity of entityType weather station. We can also model the thermometer at the weather station as an Entity of entityType Sensor. Alternatively, we can be even more specific and add the entityType as Thermometer. In this example, we'll add thermometer as an entityTag.

```json
{
  "@context": {
    "resco": "http://github.com/vibranium-data/resco",
    "schema": "http://schema.org#"
  },
    {
      "@id": "resco:Entity/S108",
      "@type": "resco:Entity",
      "resco:entityId": "S108",
      "resco:entityName": "Marina Gardens Drive Weather Station",
      "resco:entityType": "WeatherStation",
      "resco:entityTag": ["weather", "marina gardens", "singapore"],
      "resco:hasCondition": "resco:Condition/operational"
    }
}

```

```json
{
  "@id": "resco:Entity/S108",
  "@type": "resco:Entity",
  "resco:entityId": "thermometer-S108",
  "resco:entityName": "Thermometer - Marina Gardens Drive Weather Station",
  "resco:entityType": "Sensor",
  "resco:entityTag": ["thermometer", "temperature", "singapore"],
  "resco:hasCondition": "resco:Condition/operational"
}
```

**Thermometer Condition in RESCO (JSON-LD)**

```json
{
  "@id": "resco:Condition/operational",
  "@type": "resco:Condition",
  "resco:conditionId": "operational",
  "resco:conditionLabel": "Operational",
  "resco:conditionOptions": [
    "Operational",
    "Under Maintenance",
    "Not Responding",
    "Offline"
  ],
  "resco:appliesTo": "resco:Entity/thermometer-S108"
}
```

**Temperature Readings as Measurements**

We can then model the temperature reading from the thermometer at the weather station as a Measurement.

```json
{
  "@id": "resco:Measurement/S108-2024-07-16T15:59:00Z",
  "@type": "resco:Measurement",
  "resco:measurementId": "S108-2024-07-16T15:59:00Z",
  "resco:measurementLabel": "Air Temperature",
  "resco:measurementValue": 29,
  "resco:measurementUnit": "°C",
  "resco:measurementTime": "2024-07-16T15:59:00Z",
  "resco:generatedBy": "resco:Entity/thermometer-S108"
}
```

**Relative Humidity in RESCO**
Here's another example of a weather reading in RESCO, this time of humidity measured in Singapore.
You can find the Singapore weather data from their open data [here](https://data.gov.sg/datasets/d_2d3b0c4da128a9a59efca806441e1429/view).

**Weather Station and Humidity Sensors as Entities**

We again model each weather station as an Entity, along with each humidity sensor. We use the entityType property to specify the type of entity, and entityTag properties to include additional labels relevant to practitioners, researchers or administrators.
We also expand RESCO to include an entityLocation property for the weather station, showing RESCO's easy customizability.

```json
{
  "@context": {
    "resco": "http://github.com/vibranium-data/resco",
    "schema": "http://schema.org/"
  },
    {
      "@id": "resco:Entity/S108",
      "@type": "resco:Entity",
      "resco:entityId": "S109",
      "resco:entityName": "Ang Mo Kio Avenue 5 Weather Station",
      "resco:entityType": "WeatherStation",
      "resco:entityLocation": {"lat":"1.3764","long":"103.8492"},
      "resco:entityTag": ["weather", "ang mo kio", "singapore"],
      "resco:hasCondition": "resco:Condition/operational"
    }
}

```

```json
{
  "@id": "resco:Entity/S109",
  "@type": "resco:Entity",
  "resco:entityId": "humidity-sensor-S109",
  "resco:entityName": "Hygrometer - Marina Gardens Drive Weather Station",
  "resco:entityType": "Sensor",
  "resco:entityTag": ["hygrometer", "humidity", "singapore"],
  "resco:hasCondition": "resco:Condition/operational"
}
```

**Hygrometer (Humidity Sensor) Condition in RESCO (JSON-LD)**

```json
{
  "@id": "resco:Condition/operational",
  "@type": "resco:Condition",
  "resco:conditionId": "operational",
  "resco:conditionLabel": "Operational",
  "resco:conditionOptions": [
    "Operational",
    "Under Maintenance",
    "Not Responding",
    "Offline"
  ],
  "resco:appliesTo": "resco:Entity/humidity-sensor-S109"
}
```

{
"code": 0,
"data": {
"stations": [
{
"id": "S109",
"deviceId": "S109",
"name": "Ang Mo Kio Avenue 5",
"location": {
"latitude": 1.3764,
"longitude": 103.8492
}
},
{
"id": "S106",
"deviceId": "S106",
"name": "Pulau Ubin",
"location": {
"latitude": 1.4168,
"longitude": 103.9673
}
},
{
"id": "S107",
"deviceId": "S107",
"name": "East Coast Parkway",
"location": {
"latitude": 1.3135,
"longitude": 103.9625
}
},
{
"id": "S115",
"deviceId": "S115",
"name": "Tuas South Avenue 3",
"location": {
"latitude": 1.29377,
"longitude": 103.61843
}
},
{
"id": "S102",
"deviceId": "S102",
"name": "Semakau Landfill",
"location": {
"latitude": 1.189,
"longitude": 103.768
}
},
{
"id": "S60",
"deviceId": "S60",
"name": "Sentosa",
"location": {
"latitude": 1.25,
"longitude": 103.8279
}
},
{
"id": "S50",
"deviceId": "S50",
"name": "Clementi Road",
"location": {
"latitude": 1.3337,
"longitude": 103.7768
}
},
{
"id": "S44",
"deviceId": "S44",
"name": "Nanyang Avenue",
"location": {
"latitude": 1.34583,
"longitude": 103.68166
}
},
{
"id": "S43",
"deviceId": "S43",
"name": "Kim Chuan Road",
"location": {
"latitude": 1.3399,
"longitude": 103.8878
}
},
{
"id": "S24",
"deviceId": "S24",
"name": "Upper Changi Road North",
"location": {
"latitude": 1.3678,
"longitude": 103.9826
}
},
{
"id": "S06",
"deviceId": "S06",
"name": "Paya Lebar",
"location": {
"latitude": 1.3524,
"longitude": 103.9007
}
},
{
"id": "S111",
"deviceId": "S111",
"name": "Scotts Road",
"location": {
"latitude": 1.31055,
"longitude": 103.8365
}
}
],
"readings": [
{
"timestamp": "2025-10-19T01:59:00+08:00",
"data": [
{
"stationId": "S109",
"value": 83.6
},
{
"stationId": "S106",
"value": 86.7
},
{
"stationId": "S107",
"value": 79.3
},
{
"stationId": "S115",
"value": 84.2
},
{
"stationId": "S102",
"value": 84.9
},
{
"stationId": "S60",
"value": 85.3
},
{
"stationId": "S50",
"value": 85.4
},
{
"stationId": "S44",
"value": 88.1
},
{
"stationId": "S43",
"value": 81.4
},
{
"stationId": "S24",
"value": 82.1
},
{
"stationId": "S06",
"value": 78
},
{
"stationId": "S111",
"value": 85.8
}
]
}
],
"readingType": "RH 1M F",
"readingUnit": "percentage"
},
"errorMsg": ""
}
