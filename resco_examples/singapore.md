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
  "@id": "resco:Measurement/S108-temp-2024-07-16T15:59:00Z",
  "@type": "resco:Measurement",
  "resco:measurementId": "S108-temp-2024-07-16T15:59:00Z",
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

**Relative Humidity Readings as Measurements**

We can then model the relative humidity reading from the thermometer at the weather station as a Measurement.

```json
{
  "@id": "resco:Measurement/S109-rh-2025-10-19T01:59:00Z",
  "@type": "resco:Measurement",
  "resco:measurementId": "S109-rh-2025-10-19T01:59:00Z",
  "resco:measurementLabel": "Relative Humidity",
  "resco:measurementValue": 83.6,
  "resco:measurementUnit": "%",
  "resco:measurementTime": "2025-10-19T01:59:00Z",
  "resco:generatedBy": "resco:Entity/thermometer-S108"
}
```

**Average Relative Humidity as an Indicator**

With relative humidity Measurements across Singapore from each weather station, we can aggregate these Measurements to generate an Indicator for the average humidity across Singapore.

```json
{
  "@id": "resco:Indicator/singapore_average_humidity",
  "@type": "resco:Indicator",
  "resco:indicatorType": "Singapore Average Relative Humidity",
  "resco:indicatorValue": 83.7,
  "resco:indicatorUnit": "%",
  "resco:basedOnMeasurement": [
    "resco:Measurement/S109-rh-2025-10-19T01:59:00Z",
    "resco:Measurement/S106-rh-2025-10-19T01:59:00Z",
    "resco:Measurement/S107-rh-2025-10-19T01:59:00Z",
    "resco:Measurement/S115-rh-2025-10-19T01:59:00Z",
    "resco:Measurement/S102-rh-2025-10-19T01:59:00Z",
    "resco:Measurement/S060-rh-2025-10-19T01:59:00Z",
    "resco:Measurement/S050-rh-2025-10-19T01:59:00Z",
    "resco:Measurement/S044-rh-2025-10-19T01:59:00Z",
    "resco:Measurement/S043-rh-2025-10-19T01:59:00Z",
    "resco:Measurement/S024-rh-2025-10-19T01:59:00Z",
    "resco:Measurement/S006-rh-2025-10-19T01:59:00Z",
    "resco:Measurement/S111-rh-2025-10-19T01:59:00Z"
  ]
}
```

---

## Example 2 - Traffic Images in RESCO

Domain: Mobility, Security

We can model traffic images taken from traffic cameras across Singapore's highway networks to analyze traffic patterns, to aid with emergency response initiatives and to aid in security measures.
Data is provided by Singapore's Land Transport Authority. You can find the data [here](https://data.gov.sg/datasets/d_6cdb6b405b25aaaacbaf7689bcc6fae0/view).

**Cameras as Entities**

We model each camera as an Entity of entityType Sensor.

```json
{
  "@context": {
    "resco": "http://github.com/vibranium-data/resco",
    "schema": "http://schema.org/"
  },
    {
      "@id": "resco:Entity/camera-C1001",
      "@type": "resco:Entity",
      "resco:entityId": "C1001",
      "resco:entityName": "traffic_camera_1001",
      "resco:entityType": "Sensor",
      "resco:entityLocation": {"lat":"1.29531332","long":"103.871146"},
      "resco:entityTag": ["camera", "traffic", "singapore"],
      "resco:hasCondition": "resco:Condition/camera-operational-status"
    }
}

```

**Camera Condition in RESCO (JSON-LD)**

```json
{
  "@id": "resco:Condition/camera-operational-status",
  "@type": "resco:Condition",
  "resco:conditionId": "operational",
  "resco:conditionLabel": "Operational",
  "resco:conditionOptions": [
    "Operational",
    "Under Maintenance",
    "Not Responding",
    "Offline"
  ],
  "resco:appliesTo": "resco:Entity/camera-C1001"
}
```

**Image Records as Measurements**

From each camera, we can model every image the camera takes as a Measurement. This way, we can associate each image with the time it was taken via a timestamp, and with the camera that took it through Measurement properties. We expand RESCO's core set of Measurement properties to include a measurementURL property that points to the location of the raw image's storage.

```json
{
  "@id": "resco:Measurement/C1001-img-2025-10-20T20:26:05Z",
  "@type": "resco:Measurement",
  "resco:measurementId": "C1001-img-2025-10-20T20:26:05Z",
  "resco:measurementLabel": "Traffic Camera Feed",
  "resco:measurementValue": "",
  "resco:measurementUnit": "",
  "resco:measurementTime": "2025-10-20T20:26:05Z",
  "resco:measurementURL": "https://images.data.gov.sg/api/traffic-images/2025/10/1e12ec16-3c48-47bb-b687-97235853401d.jpg",
  "resco:generatedBy": "resco:Entity/camera-C1001"
}
```

Because of RESCO's expandable set of properties, it is also posssible to expand RESCO class properties to add other properties such as image metadata and addresses. With clear relationships of Measurements to Entities, it is also easy to perform tasks such as aggregations for specific locations, to define networks and to define machine learning modeling pipelines in reusable templates.
