## Example: Bengaluru / Bangalore EV Charging Stations

Domain: Energy. Mobility

Data Source: [Bengaluru Open Data Portal](https://opendata.benscl.com/?q=dataset/ev-stations)

**EV Stations as Entities**

We can model each EV charging station as an Entity of entityType EV Charging Station. We can also extend RESCO's core Entity properties to include an entityLocation property which enables us to include each EV station's coordinates. Finally, we're also able to use the flexible entityTag property on each EV station to help add context, such as with adding particular company brands that own and/or operate the EV station. We can also add a tag to show whether there are additional services related to EV charging at a station, such as battery swaps.

```json
{
  "@context": {
    "resco": "http://github.com/vibranium-data/resco",
    "schema": "http://schema.org#"
  },
    {
      "@id": "resco:Entity/ev_st0000001",
      "@type": "resco:Entity",
      "resco:entityId": "ev_st0000001",
      "resco:entityName": "BESCOM - Hosakote SDO",
      "resco:entityType": "ev-charging-station",
      "resco:entityLocation": {"lat":"13.0731299","long":"77.786843"},
      "resco:entityTag": ["BESCOM", "ev station", "bengaluru", "battery swap available"],
      "resco:hasCondition": "resco:Condition/ev-station-operational-status"
    }
}

```

**EV Station Operational Status as Conditions**

We can then model each EV station's operational status as a Condition, to understand whether the EV station is available to provide charging services and also to monitor and schedule maintenance projects. This data could then be used in other applications, foe example to show drivers available and operational EV stations near them.

```json
{
  "@id": "resco:Condition/ev-station-operational-status",
  "@type": "resco:Condition",
  "resco:conditionId": "operational",
  "resco:conditionLabel": "Operational",
  "resco:conditionOptions": [
    "Operational",
    "Under Maintenance",
    "Not Responding",
    "Offline"
  ],
  "resco:appliesTo": "resco:Entity/ev-station-operational-status"
}
```
