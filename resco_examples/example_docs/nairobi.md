## Example: Nairobi Air Quality

Domain: Climate / Environment

Data source: [Sensors.Africa Air Quality Data](https://sensors.africa/air/city/nairobi)

**Sensors as Entities**
We model the air quality sensors in Nairobi's Central Business District (CBD) to generate PM10 air quality measurements at each CBD station.
Sensors are treated as Entities with entityType as _"Sensor"_ that generate Measurements.

```json
{
  "@context": {
    "resco": "https://github.com/vibranium-data/resco",
    "schema": "http://schema.org/"
  },
  "@id": "resco:Entity/nbo-sensor-000004849",
  "@type": "resco:Entity",
  "resco:entityType": "AirQualitySensor",
  "resco:hasMeasurement": {
    "@id": "resco:Measurement/nbo-cbd-sensor-000004849-pm10",
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
  "@id": "resco:Condition/nbo-cbd-sensor-000004849-status",
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

We aggregate the air quality measurements from every sensor in the Central Business District to generate an Air Quality Index localized to this region of the city. We can then compare air quality metrics across different regions in the city, as well as aggregate measurements across all of the city's sensors to generate an Air Quality Index.

Here, we model the Air Quality Index at Nairobi's Central Business District by aggregating Measurements from three sensors.

```json
{
  "@id": "resco:Indicator/nbo-cbd-pm10-aqi",
  "@type": "resco:Indicator",
  "resco:indicatorType": "AirQualityIndex",
  "resco:indicatorValue": 38,
  "resco:indicatorUnit": "AQI",
  "resco:indicatesCondition": "resco:Condition/nbo-pm10-quality",
  "resco:basedOnMeasurement": [
    "resco:resco:Measurement/nbo-sensor-000004849-pm10",
    "resco:resco:Measurement/nbo-sensor-000000049-pm10",
    "resco:resco:Measurement/nbo-sensor-000004980-pm10"
  ]
}
```

**Environmental Condition in RESCO (JSON-LD)**

We can then model a Condition for the air quality in Nairobi's CBD for continuous monitoring, evaluation and reporting across the city.

```json
{
  "@id": "resco:Condition/nbo-cbd-pm10-quality",
  "@type": "resco:Condition",
  "resco:conditionTag": "environment",
  "resco:conditionLabel": "Air Quality Condition",
  "resco:conditionOptions": "['Good', 'Moderate', 'Poor']",
  "resco:conditionValue": "Good"
}
```

---

## Example: Nairobi GTFS Matatu Routes

Domain: Mobility

Data source: [Nairobi Digital Matatus Project, Gitlab](https://gitlab.com/digitaltransport/data/africa/nairobi/-/blob/master/Data/GTFS.zip?ref_type=heads)

**Bus / Matatu Stops as Entities**

We model each stop along matatu routes as Entities using some of the base properties. We use custom properties on the Entity class, which we can easily expand RESCO to include, so as to add location data to each stop.

```json
{
  "@context": {
    "resco": "https://github.com/vibranium-data/resco",
    "schema": "http://schema.org/"
  },
  "@id": "resco:Entity/nbo-bus-stop-0001RLW",
  "@type": "resco:Entity",
  "resco:entityType": "Bus Stop",
  "resco:entityName": "Railways",
  "resco:entityLatitude": "-1.290884",
  "resco:entityLongitude": "36.828242"
}
```

**Matatu / Bus Trip as Event**

Each matatu or bus trip is modeled as an Event, involving the bus or matatu and the departure and arrival stations as entities.
We can also model the departure and arrival times of the matatus as Measurements, matching each measurement with its associated trip Event.

```json
{
  "@id": "resco:Event/matatu-trip-koja-banana-10300106011",
  "@type": "resco:Event",
  "resco:eventType": "MatatuTrip",
  "resco:eventTime": "2025-09-30T10:00:00Z",
  "resco:generatedBy": "resco:Entity/matatu-000KBR436W",
  "resco:involvedEntity": [
    "resco:Entity/matatu-000KBR436W",
    "resco:Entity/koja-bus-stop-0001KJA",
    "resco:Entity/banana-bus-stop-0001BNA"
  ],
  "resco:hasMeasurement": [
    "resco:Measurement/departure-koja-bus-stop-0001KJA",
    "resco:Measurement/arrival-banana-bus-stop-0001BNA"
  ]
}
```
