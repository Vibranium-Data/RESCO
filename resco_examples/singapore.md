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
    "xsd": "http://www.w3.org/2001/XMLSchema#"
  },
    {
      "@id": "resco:Entity/S108",
      "@type": "resco:Entity",
      "resco:entityId": "S108",
      "resco:entityName": "Marina Gardens Drive Weather Station",
      "resco:entityType": "Sensor",
      "resco:entityTag": "weather, temperature, singapore",
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

    {
      "@id": "resco:Measurement/S108-2024-07-16T15:59:00Z",
      "@type": "resco:Measurement",
      "resco:measurementId": "S108-2024-07-16T15:59:00Z",
      "resco:measurementLabel": "Air Temperature",
      "resco:measurementValue": 29,
      "resco:measurementUnit": "°C",
      "resco:measurementTime": "2024-07-16T15:59:00Z",
      "resco:generatedBy": "resco:Entity/S108"
    }

]
}
