# RESCO: Reduced Set City Ontology

## Introduction

**Reduced Set City Ontology (RESCO)** is a **minimal yet extensible ontology** for urban data integration, supporting interoperability, reusability, reproducibility, replicability and system-wide monitoring across a variety of urban domains. RESCO emphasizes:

- **Simplicity**: a reduced set of interoperable classes that practitioners can readily adopt.
- **Expressiveness**: enough semantic rigor to represent urban dynamics, not just static assets.
- **Scalability**: adaptable to both data-rich and resource-constrained cities.
- **Interoperability**: alignment with established standards (e.g. SOSA/SSN, NGSI-LD).

---

## Core Classes

RESCO defines a small but powerful set of classes to represent infrastructure, observations, and interventions.

| **Class**        | **Definition**                                                                                                                                                   |
| ---------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Entity**       | A generic object of interest in the city (e.g. bus, building, organization, power plant, traffic light, camera, individual)                                      |
| **Measurement**  | A recorded value associated with an Entity (e.g. pm2.5 reading, voltage reading, temperature reading, car count, water level reading ).                          |
| **Indicator**    | A derived or aggregated measure used for evaluation (e.g. % buses on time, air quality index, traffic volume, total grid load).                                  |
| **Condition**    | A state or status of an entity, often qualitative (e.g. road is congested, plant is under maintenance, air quality sensor is functional, water quality is poor). |
| **Event**        | A discrete occurrence emitted by or affecting entities, or their conditions (e.g. sensor reading, road maintenance, flood, traffic congestion, blackout).        |
| **Intervention** | An action taken to influence system performance (e.g. deploying buses, adjusting water pumping, updating train schedules, rerouting power transmission).         |

---

## Design Principles

1. **Reduced Set Philosophy**

   - Minimalism with Expressiveness: Only the most essential classes are defined.
   - Avoids unnecessary complexity while remaining expressive.

2. **Open World Assumption (OWA)**

   - Knowledge is not assumed complete: the ontology is extensible by practitioners, developers for their custom needs.
   - Useful for urban data integration, where datasets are fragmented and partial.

3. **Alignment with Standards**
   - Maps to existing frameworks such as SOSA/SSN and NGSI-LD.
   - Provides a lightweight entry point for practitioners while staying interoperable with other ontologies.

---

## Example: Sensors in RESCO

Sensors are treated as **Entities** that generate **Measurements**.  
Entities would have **entityType** as **"Sensor"**
Examples of sensors include:

- Environmental: Air quality sensor, thermometer, weather station instrument(s)
- Mobility: GPS unit on buses, traffic camera, lidar sensor
- Utilities: Smart water meter, smart grid monitor

**JSON-LD Example (Air Quality Sensor as a sensor):**

```json
{
  "@context": {
    "resco": "https://example.org/resco#",
    "schema": "http://schema.org/"
  },
  "@id": "resco:Entity/nyc-sensor-001234567",
  "@type": "resco:Entity",
  "resco:entityType": "AirQualitySensor",
  "resco:hasMeasurement": {
    "@id": "resco:Measurement/nyc-sensor-001-pm25",
    "@type": "resco:Measurement",
    "resco:measurementLabel": "e.g. PM2.5 concentration (µg/m³)",
    "resco:measurementValue": 12.3,
    "resco:measurementUnit": "µg/m³",
    "resco:measurementTimestamp": "2025-09-09T08:30:00Z",
    "resco:measurementLabel": "e.g. PM2.5 concentration (µg/m³)"
  }
}
```

**Infrastructure Condition in RESCO (JSON-LD)**

```json
{
  "@id": "resco:Condition/nyc-sensor-001-status",
  "@type": "resco:Condition",
  "resco:conditionTag": "infrastructure",
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
  "@id": "resco:Indicator/nyc-pm25-aqi",
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
  "@id": "resco:Condition/nyc-pm25-quality",
  "@type": "resco:Condition",
  "resco:conditionTag": "environment",
  "resco:conditionLabel": "Air Quality Condition",
  "resco:conditionOptions": "['Good', 'Moderate', 'Poor']",
  "resco:conditionValue": "Good"
}
```
