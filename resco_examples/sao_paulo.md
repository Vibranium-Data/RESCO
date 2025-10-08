## Example: Sao Paulo and Rio de Janeiro Energy - Grid Supply and Demand

Domain: Energy

Data source: [IPDO-ONS Balance of Energy Reports](./data_sources/IPDO-22-09-2025.pdf)

### 1. Sao Paulo and Rio de Janeiro Grid Energy Supply

**Power Plant as Entity**

Each power is modeled as an Entity. Here, we have each dam associated with an energy reading, read by the power plant's meters. We can either model the power plant's meters granularly, meter by meter, or the power plant overall and its associated total capacity. We can have different types of entities - from organizations, systems composed of different machines, to even individual actors, so we use the entityType label to show that we are modeling a Power Plant. Sao Paulo and Rio de Janeiro get power from varying energy sources - hydropower, oil and gas, nuclear, bioenergy, solar and wind, so we use the entityTag to label the type of power plant. The data source reports the energy supplied by each power plant in megawatts (MW), so we use that for the Measurement.

```json
{
  "@context": {
    "resco": "https://www.github.com/vibranium-data/resco",
    "schema": "http://schema.org/"
  },
  "@id": "resco:Entity/angra-ii-005",
  "@type": "resco:Entity",
  "resco:entityType": "Power Plant",
  "resco:entityTag": "Nuclear"
  "resco:hasMeasurement": {
    "@id": "resco:Measurement/angra-ii-002",
    "@type": "resco:Measurement",
    "resco:measurementLabel": "Available Power Capacity (MW)",
    "resco:measurementValue": 1350.0,
    "resco:measurementUnit": "megawatts",
    "resco:measurementTimestamp": "2025-09-22T05:00:00Z"
  }
}
```

**Power Plant Condition**

We can model the power plant's condition to monitor infrastructure and schedule maintenance across the grid.

```json
{
  "@id": "resco:Condition/angra-ii-005-status",
  "@type": "resco:Condition",
  "resco:conditionTag": "Energy Infrastructure",
  "resco:conditionLabel": "Power Plant operational status",
  "resco:conditionValue": "Operational",
  "resco:conditionOptions": ["Operational", "Under Maintenance", "Closed"],
  "resco:appliesTo": "Entity/angra-ii-005"
}
```
