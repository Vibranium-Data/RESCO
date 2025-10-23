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
      "resco:entityTag": ["cargo ship", "port-of-barcelona", "netherlands"],
      "resco:hasCondition": "resco:Condition/ship-operational-status"
    }
}
```

**Ship Operation Status as Conditions**

We can model the operational status of each ship as a Condition. This can help the port monitor and share information on whether the ship is functioning, and even in processing repair requests.

```json
{
  "@id": "resco:Condition/ship-operational-status",
  "@type": "resco:Condition",
  "resco:conditionId": "ship-operational",
  "resco:conditionLabel": "Operational",
  "resco:conditionOptions": [
    "Operational",
    "Under Maintenance",
    "Malfunctioning"
  ],
  "resco:conditionTag": "normal"
}
```

**Ship Arrivals and Departures as Events**

We can model each ship's arrival and departure as Events in RESCO.

```json
{
  "@id": "resco:Event/ship-arrival-2025-10-21",
  "@type": "resco:Event",
  "resco:eventId": "ship-arrival-2025-10-21",
  "resco:involvedEntity": "resco:Entity/ship-AMELAND",
  "resco:eventTime": "2025-10-21T11:34:00Z",
  "resco:generatedByEvent": "resco:Entity/Port-of-Barcelona",
  "resco:entityTag": ["arrival", "port-call", "eta"]
}
```

```json
{
  "@id": "resco:Event/ship-departure-2025-10-22",
  "@type": "resco:Event",
  "resco:eventId": "ship-departure-2025-10-22",
  "resco:involvedEntity": "resco:Entity/ship-AMELAND",
  "resco:eventTime": "2025-10-22T19:00:00Z",
  "resco:generatedByEvent": "resco:Entity/Port-of-Barcelona",
  "resco:entityTag": ["departure", "port-call", "etd"]
}
```

**Measurements from Arrivals and Departures**

We can model Arrival and Departure times as Measurements, either from the Arrival and Departure Events or directly from the port.

Here, we use the unit of an epoch timestamp for the measurementValue.

```json
{
  "@id": "resco:Measurement/ship-ameland-ETA",
  "@type": "resco:Measurement",
  "resco:measurementLabel": "Number of Customers affected",
  "resco:measurementValue": 1761046440.0,
  "resco:measurementUnit": "seconds",
  "resco:measurementTime": "2025-10-21T11:34:00Z",
  "resco:measuredBy": "resco:Entity/ship-AMELAND",
  "resco:appliesTo": "resco:Entity/ship-AMELAND"
}
```
