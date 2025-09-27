## Example: New York MTA - Subway

Domain: Mobility

Data source: [New York MTA GTFS Data](https://data.ny.gov/Transportation/MTA-General-Transit-Feed-Specification-GTFS-Static/fgm6-ccue/about_data)

**Subway Trip as Event**

Each subway trip is modeled as an Event, involving the train and the departure and arrival stations as entities.

```json
{
  "@id": "resco:Event/mta-trip-127-A27-1",
  "@type": "resco:Event",
  "resco:eventType": "SubwayTrip",
  "resco:eventTime": "2025-09-26T08:30:00Z",
  "resco:generatedBy": "resco:Entity/train-001",
  "resco:involvedEntity": [
    "resco:Entity/train-001",
    "resco:Entity/station-127",
    "resco:Entity/station-A27"
  ],
  "resco:hasMeasurement": [
    "resco:Measurement/departure-127-A27-1",
    "resco:Measurement/arrival-127-A27-1"
  ]
}
```

**Subway Departure Time and Arrival Time as Measurements**

Departure Time and Arrival Times are emitted as Measurements by the train when it leaves its departure station and arrives at its arrival station.

```json
{
  "@id": "resco:Measurement/departure-127-A27-1",
  "@type": "resco:Measurement",
  "resco:measurementLabel": "Departure Time",
  "resco:measurementValue": "2025-09-26T08:30:00Z",
  "resco:measurementUnit": "ISO8601",
  "resco:measurementTime": "2025-09-26T08:30:00Z"
}
```

```json
{
  "@id": "resco:Measurement/arrival-127-A27-1",
  "@type": "resco:Measurement",
  "resco:measurementLabel": "Arrival Time",
  "resco:measurementValue": "2025-09-26T08:34:40Z",
  "resco:measurementUnit": "ISO8601",
  "resco:measurementTime": "2025-09-26T08:34:40Z"
}
```

**Subway Trip Duration as an Indicator**

The trip duration for a specific trip is derived from two _Measurements_: That particular trip's Arrival Time and Departure Time.

```json
{
  "@id": "resco:Indicator/tripDuration-127-A27-1",
  "@type": "resco:Indicator",
  "resco:indicatorLabel": "Trip Duration (127 → A27)",
  "resco:indicatorValue": 280,
  "resco:indicatorUnit": "seconds",
  "resco:indicatesCondition": "Trip Duration SLA",
  "resco:basedOnMeasurement": [
    "resco:Measurement/departure-127-A27-1",
    "resco:Measurement/arrival-127-A27-1"
  ]
}
```

**Average Trip Duration for A Particular Route**

To get a high-level indicator for average trip duration, we aggregate Trip Durations for that particular route.
If we have 3 different trips from station 127 to A27, trip 1, trip 2 and trip 3, we average out their trip durations to model the average trip duration for trips from station 127 to A27.

```json
{
  "@id": "resco:Indicator/avg-tripDuration-127-A27",
  "@type": "resco:Indicator",
  "resco:indicatorLabel": "Average Transfer Time (127 → A27)",
  "resco:indicatorValue": 295,
  "resco:indicatorUnit": "seconds",
  "resco:basedOnMeasurement": [
    "resco:Indicator/tripDuration-127-A27-1",
    "resco:Indicator/tripDuration-127-A27-2",
    "resco:Indicator/tripDuration-127-A27-3"
  ]
}
```

**Subway Trip Status as a Condition**

If we have expected arrival times included based on a subway schedule, we can also have trip statuses as Conditions.
These could include trip statuses such as: _On Time_, _Early_, _Late_.
Here, the Condition is based on a trip Event, indicated by the optional _derivedFrom_ property.

```json
{
  "@id": "resco:Condition/tripStatus-127-A27-1",
  "@type": "resco:Condition",
  "resco:conditionLabel": "Trip Status",
  "resco:conditionValue": "On Time",
  "resco:conditionOptions": ["On Time", "Early", "Late"],
  "resco:conditionTag": "MTA Subway Trip Statuses",
  "resco:appliesTo": "resco:Event/mta-trip-127-A27-1",
  "resco:derivedFrom": "resco:Indicator/tripDuration-127-A27-1"
}
```

**Subway Trip Duration SLA as a Condition**

We can model whether a trip arrived within its standard SLA, based on its Trip Duration Indicator.
For this SLA, we condition options _SLA Met: Standard_, _SLA Met: Above Expectations_, _SLA Unmet: Below Expectations_.
We can also add tags for quick filtering, say if there are different SLA Trackers across systems or organizations.

```json
{
  "@id": "resco:Condition/tripDurationSLA-127-A27-1",
  "@type": "resco:Condition",
  "resco:conditionLabel": "Trip Duration SLA",
  "resco:conditionValue": "SLA Met: Standard",
  "resco:conditionOptions": [
    "SLA Met: Standard",
    "SLA Met: Above Expectations",
    "SLA Unmet: Below Expectations"
  ],
  "resco:appliesToEntity": "resco:Entity/train-001",
  "resco:conditionTag": "MTA Subway SLA Trackers",
  "resco:derivedFrom": "resco:Indicator/tripDuration-127-A27-1"
}
```
