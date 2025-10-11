## Example: Nairobi Air Quality

Domain: Climate / Environment

Data source: [Sensors.Africa Air Quality Data](https://sensors.africa/air/city/nairobi)

**Sensors as Entities**

Sensors are treated as Entities with entityType as _"Sensor"_ that generate Measurements.

```json
{
  "@context": {
    "resco": "https://github.com/vibarnium-data/resco",
    "schema": "http://schema.org/"
  },
  "@id": "resco:Entity/nbo-sensor-000004849",
  "@type": "resco:Entity",
  "resco:entityType": "AirQualitySensor",
  "resco:hasMeasurement": {
    "@id": "resco:Measurement/nbo-sensor-000004849-pm10",
    "@type": "resco:Measurement",
    "resco:measurementLabel": "PM10 concentration (µg/m³)",
    "resco:measurementValue": 43.0,
    "resco:measurementUnit": "µg/m³",
    "resco:measurementTimestamp": "2025-03-22T10:00:00Z"
  }
}
```

**Infrastructure Condition in RESCO (JSON-LD)**

```json
{
  "@id": "resco:Condition/nbo-sensor-000004849-status",
  "@type": "resco:Condition",
  "resco:conditionTag": "air quality infrastructure",
  "resco:conditionLabel": "Sensor operational status",
  "resco:conditionValue": "Operational",
  "resco:conditionOptions": [
    "Operational",
    "Under Maintenance",
    "Not Responding",
    "Offline"
  ]
}
```

**Indicator Representation in RESCO (JSON-LD)**

```json
{
  "@id": "resco:Indicator/nbo-pm25-aqi",
  "@type": "resco:Indicator",
  "resco:indicatorType": "AirQualityIndex",
  "resco:indicatorValue": 42,
  "resco:indicatorUnit": "AQI",
  "resco:indicatesCondition": "resco:Condition/nyc-pm25-quality"
}
```

**Environmental Condition in RESCO (JSON-LD)**

```json
{
  "@id": "resco:Condition/nbo-pm25-quality",
  "@type": "resco:Condition",
  "resco:conditionTag": "environment",
  "resco:conditionLabel": "Air Quality Condition",
  "resco:conditionOptions": "['Good', 'Moderate', 'Poor']",
  "resco:conditionValue": "Good"
}
```
