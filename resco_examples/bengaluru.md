## Example: Bengaluru / Bangalore EV Charging Stations

Domain: Energy. Mobility

Data Source: [Bengaluru Open Data Portal](https://opendata.benscl.com/?q=dataset/ev-stations)

**EV Stations as Entities**

We can model each EV charging station as an Entity of entityType EV Charging Station. We can also extend RESCO's core Entity properties to include an entityLocation property which enables us to include each EV station's coordinates. Finally, we're also able to use the flexible entityTag property on each EV station to help add context, such as with adding particular company brands that own and/or operate the EV station.

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
      "resco:entityTag": ["BESCOM", "ev station", "bengaluru"],
      "resco:hasCondition": "resco:Condition/ev-station-operational-status"
    }
}

```
