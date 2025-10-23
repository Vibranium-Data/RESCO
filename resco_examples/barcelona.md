## Example: Barcelona -- Port of Barcelona

Domain: Mobility, Ports

Data Source: [Port of Barcelona Daily Shipping Docks Open Data](https://opendata.portdebarcelona.cat/es/dataset/vaixells-en-port)
Archived Data Source [here](./data_sources/port_barcelona_docking_data.csv).

We can use RESCO to model port operations, which would be useful for urban practitioners focused on port cities or port operations. In this example, we'll walk through modeling port data for the Port of Barcelona. We'll focus on docking data for ships at the Port of Barcelona, showing how RESCO can model the ships' arrivals and departures along with other port operations.

**Ships as Entities**

We model each of the sea vessels that dock at the port as Entities, of entityType Vessel.

```json
{
  "@context": {
    "resco": "http://github.com/vibranium-data/resco",
    "xsd": "http://www.schema.org/"
  },
    {
      "@id": "resco:Entity/ship-AMELAND",
      "@type": "resco:Entity",
      "resco:entityId": "9508794",
      "resco:entityName": "AMELAND",
      "resco:entityType": "Vessel",
      "resco:entityTag": ["cargo", "port-of-barcelona", "netherlands"],
      "resco:hasCondition": "resco:Condition/ship-operational"
    }
}
```
