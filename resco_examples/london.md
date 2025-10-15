## Example: London Traffic - Road Disruptions

Domain: Mobility

Data source: [Transport for London (TFL) Data](https://tfl.gov.uk/info-for/open-data-users/our-open-data)
Register for the TFL API to gain access [here](https://api-portal.tfl.gov.uk/).

### 1. London Road Traffic Disruptions as Events

**Roads as Entities**
We can model each road in the Transport for London network as an Entity, of entityType RoadSegment. We can even further expand RESCO to accomodate subtypes if needed, or use an entityTag to label this Entity as a road.

```json

{
  "@context": {
    "resco": "http://github.com/vibranium-data/resco",
    "schema": "http://schema.org/"
  },
    {
      "@id": "resco:Entity/a316-burlington-lane",
      "@type": "resco:Entity",
      "resco:entityType": "RoadSegment",
      "resco:entityName": "[A316] Burlington Lane (W4)",
      "resco:entityId": "road-a316-burlington-lane",
      "resco:entityTag": ["Asset", "Transport", "Road"],
      "resco:hasCondition": "resco:Condition/a316-burlington-lane-status"
    }
}
```

**Road Conditions to Report Operational Status**

We can use Conditions for each road segment to report on its operational status. In this case, the road has been closed, which is why there is a traffic disruption reported.

```json
{
  "@id": "resco:Condition/a316-burlington-lane-status",
  "@type": "resco:Condition",
  "resco:conditionLabel": "Operational Status",
  "resco:conditionTag": ["infrastructure", "Northbound"],
  "resco:conditionValue": "Closed",
  "resco:conditionOptions": [
    "Operational",
    "Operational - Maintenance Ongoing",
    "Closed"
  ],
  "resco:appliesTo": "resco:Entity/a316-burlington-lane"
}
```

**Traffic Disruptions as Events**

We can model traffic disruptions on London roads as Events in RESCO. Here, we model the traffic disruption as an Event while also expanding the Event properties to include custom properties such as:

- A description under eventDescription
- A rating of the disruption's severity under eventSeverity
- A custom update message by public works operators for the event under eventUpdate

```json
{
  "@id": "resco:Event/tims-217284",
  "@type": "resco:Event",
  "resco:eventType": "Utility Works",
  "resco:eventId": "TIMS-217284",
  "resco:eventTime": "2025-09-28T19:00:00Z",
  "resco:involvedEntity": "resco:Entity/a316-burlington-lane",
  "resco:generatedByEvent": "resco:Entity/tfl",
  "resco:eventSeverity": "Moderate",
  "resco:eventDescription": "Emergency gas main repairs at [A316] Burlington Lane northbound at the junction of [A4] Hogarth Lane. No northbound access to Hogarth Roundabout. Hogarth Flyover remains open.",
  "resco:eventUpdate": "Delays possible; status active as of 2025-10-15T14:52:00Z",
  "resco:eventTag": ["Works", "Utility", "Gas"]
}
```

**TFL as Entity**

We can model participating organizations, such as Transport for London(TFL), cities, or local governments as Entities. Here, we provide an example of modeling TFL as an Entity.

```json
{
  "@id": "resco:Entity/tfl",
  "@type": "resco:Entity",
  "resco:entityType": "Organization",
  "resco:entityName": "Transport for London (TfL)",
  "resco:entityId": "org-tfl"
}
```
