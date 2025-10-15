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

We can model the operational status of each power distribution zone, reporting whether each substation is operational, under maintenance or offline as needed.

```json
{
  "@id": "resco:Condition/kingston-zone-status",
  "@type": "resco:Condition",
  "resco:conditionLabel": "Grid operational status",
  "resco:conditionTag": "infrastructure",
  "resco:conditionValue": "Faulted (11kV cable failure)",
  "resco:conditionOptions": ["Operational", "Under Maintenance", "Offline"],
  "resco:appliesTo": "resco:Entity/kingston-zone-0000swldn"
}
```

    {
      "@id": "resco:Event/incd-420564-g",
      "@type": "resco:Event",
      "resco:eventId": "INCD-420564-G",
      "resco:eventType": "Unplanned Power Cut",
      "resco:eventSeverity": "Moderate",
      "resco:eventTime": {
        "start": "2025-10-15T13:13:28Z",
        "expectedEnd": "2025-10-16T00:30:00Z"
      },
      "resco:involvedEntity": "resco:Entity/kingston-zone",
      "resco:eventDescription": "An underground electricity cable faulted on the high voltage network, causing an area-wide power cut. Engineers estimate most supplies will be restored by 00:30 on 16 Oct 2025.",
      "resco:eventTag": ["Energy", "Fault", "HighVoltage", "Unplanned"],
      "resco:generatedByEvent": "resco:Entity/ukpn"
    },

    {
      "@id": "resco:Measurement/incd-420564-g-affected-customers",
      "@type": "resco:Measurement",
      "resco:measurementLabel": "Customers affected",
      "resco:measurementValue": 0,
      "resco:measurementUnit": "count",
      "resco:measurementTime": "2025-10-15T13:13:28Z",
      "resco:measuredBy": "resco:Entity/ukpn",
      "resco:appliesTo": "resco:Entity/kingston-zone"
    },

    {
      "@id": "resco:Entity/ukpn",
      "@type": "resco:Entity",
      "resco:entityId": "org-ukpn",
      "resco:entityType": "Organization",
      "resco:entityName": "UK Power Networks",
      "resco:entityTag": ["Utility", "Energy"]
    }

]
}
