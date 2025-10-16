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

---

## Example: London Grid - Power Disruptions and Restoration

Domain: Energy / Grid

Data source: [UK Power Networks Live Faults Dataset](https://ukpowernetworks.opendatasoft.com/explore/dataset/ukpn-live-faults/table/)

**Grid Substations / Network Zones as Entities**

UK Power Networks distributes energy through distinct zones. We model each substation or network zone that distributes power to consumers as an Entity of entityType Power Distribution Zone. Here, we model the Kingston zone located in Southwest London as an Entity.

```json
{
  "@context": {
    "resco": "http://github.com/vibranium-data/resco"
  },
    {
      "@id": "resco:Entity/kingston-zone",
      "@type": "resco:Entity",
      "resco:entityId": "entity-kingston-zone-0000swldn",
      "resco:entityName": "Kingston Zone",
      "resco:entityType": "Power Distribution Zone",
      "resco:entityTag": ["Energy", "Grid", "UKPowerNetworks"],
      "resco:hasCondition": "resco:Condition/kingston-zone-status"
    }
}
```

**Grid Operational Status as Condition**

We can model the operational status of each power distribution zone, reporting whether each substation is operational, faulted, under maintenance or offline as needed.

```json
{
  "@id": "resco:Condition/kingston-zone-status",
  "@type": "resco:Condition",
  "resco:conditionLabel": "Grid operational status",
  "resco:conditionTag": ["infrastructure" "11kv power failure"],
  "resco:conditionValue": "Faulted",
  "resco:conditionOptions": ["Operational", "Faulted", "Under Maintenance", "Offline"],
  "resco:appliesTo": "resco:Entity/kingston-zone-0000swldn"
}
```

**Power Disruptions as Events**

We can model grid faults or other kinds of power disruptions as Events, indicating their type using the eventType property with each Event as needed. Beyond the standard Event properties, we can also add custom properties to RESCO that are beneficial to operators, reporting teams or responders as needed. In this example, we model each power disruption as an Event and add custom properties for:

- eventSeverity to indicate the severity and, therefore, the priority of the disruption
- eventDescription to include an informative description of the power disruption Event
- eventLocation to add lat/long coordinates for mapping and/or navigating as needed by city teams

```json
{
  "@id": "resco:Event/incd-420564-g",
  "@type": "resco:Event",
  "resco:eventId": "INCD-420564-G",
  "resco:eventType": "Unplanned Power Cut",
  "resco:eventSeverity": "Moderate",
  "resco:eventTime": "2025-10-15T13:13:28Z",
  "resco:involvedEntity": "resco:Entity/kingston-zone",
  "resco:entityLocation": { "lon": "-0.53765", "lat": "51.17998" },
  "resco:eventDescription": "An underground electricity cable faulted on the high voltage network, causing an area-wide power cut. Engineers estimate most supplies will be restored by 00:30 on 16 Oct 2025.",
  "resco:eventTag": ["Energy", "Fault", "HighVoltage", "Unplanned"],
  "resco:generatedByEvent": "resco:Entity/ukpn"
}
```

**Measurements for Customers**

We can have Measurements for the number of customers affected by the specific power disruption Event. This can also help with gauging severity and priority. Here, this metric is generated by the UK Power Networks.

```json
{
  "@id": "resco:Measurement/incd-420564-g-affected-customers",
  "@type": "resco:Measurement",
  "resco:measurementLabel": "Number of Customers affected",
  "resco:measurementValue": 0,
  "resco:measurementUnit": "count",
  "resco:measurementTime": "2025-10-15T13:13:28Z",
  "resco:measuredBy": "resco:Entity/ukpn",
  "resco:appliesTo": "resco:Entity/kingston-zone"
}
```

We can also similarly use Measurements to count the number of customer calls received concerning the incident.

**Organizations as Entities**

We model UK Power Networks as an Entity of type Organization, shown by its entityType property.

```json
{
  "@id": "resco:Entity/ukpn",
  "@type": "resco:Entity",
  "resco:entityId": "org-ukpn",
  "resco:entityType": "Organization",
  "resco:entityName": "UK Power Networks",
  "resco:entityTag": ["Utility", "Energy"]
}
```

**Power Restoration Time using Indicators**

We can also use Indicators to model restoration times between the time the power disruption Event is generated, and the time the power is restored.

First, we model the moment the power is confirmed as restored by UK Power Networks as an Event.

```json
{
  "@id": "resco:Event/incd-420564-g-001-restoration",
  "@type": "resco:Event",
  "resco:eventId": "incd-420564-g-001-restoration",
  "resco:eventType": "Power Restoration",
  "resco:eventTime": "2025-10-15T19:00:00Z",
  "resco:involvedEntity": "resco:Entity/kingston-zone-0000swldn",
  "resco:entityLocation": { "lon": "-0.53765", "lat": "51.17998" },
  "resco:eventDescription": "Power was restored successfully at Kingston Zone on Oct 15, 2025.",
  "resco:eventTag": ["Energy", "Restoration", "HighVoltage"],
  "resco:generatedByEvent": "resco:Entity/ukpn"
}
```

We then generate a power restoration duration Indicator based on two Measurements: power fault time and power restoration time. Each Measurement can be generated by its associated power disruption and power restoration Events.

```json
{
  "@id": "resco:Indicator/power-restoration-duration",
  "@type": "resco:Indicator",
  "resco:indicatorType": "Power Restoration Duration",
  "resco:indicatorValue": "5.78",
  "resco:indicatorUnit": "hours",
  "resco:basedOnMeasurement": [
    "resco:Measurement/power-fault-time-incd-420564-g",
    "resco:Measurement/power-restoration-time-incd-420564-g-001-restoration"
  ]
}
```

**Power Rerouting with Interventions**

We can also model Interventions by UK Power Networks to reroute power transmission using other substations or grid transmission lines to households in the Kingston zone so that there are no affected customers. This would involve RESCO's Intervention class and could be modeled as follows:

```json
{
  "@id": "resco:Intervention/restore-kingston-grid",
  "@type": "resco:Intervention",
  "resco:interventionLabel": "Grid restoration",
  "resco:implementedBy": "resco:Entity/ukpn",
  "resco:appliesTo": "resco:Entity/kingston-zone",
  "resco:basedOnIndicator": "resco:Indicator/grid-availability",
  "resco:currentEntityCondition": "resco:Condition/kingston-zone-status-faulted",
  "resco:targetEntityCondition": "resco:Condition/kingston-zone-status-operational",
  "resco:interventionStartTime": "2025-10-15T13:45:00Z",
  "resco:interventionEndTime": "2025-10-16T00:30:00Z",
  "resco:interventionOutcome": "Power Supply restored to all affected postcodes."
}
```
