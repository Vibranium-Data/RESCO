## Example: Cape Town Water Supply System

Domain: Water

Data source: [City of Cape Town Weekly Water Dashboard](https://resource.capetown.gov.za/documentcentre/Documents/City%20research%20reports%20and%20review/damlevels.pdf)

### 1. Cape Town Water Supply Dam Capacity

**Dam as Entity**

Each dam is modeled as an Entity. Here, we have each dam associated with a water volume reading, read by the dam's water meters.
We can either model the dam water meters granularly, or the dam overall and its associated total capacity.
The data source reports the volume of water stored in millions of liters, so we use that as the measurement.

```json
{
  "@context": {
    "resco": "https://example.org/resco#",
    "schema": "http://schema.org/"
  },
  "@id": "resco:Entity/theewaterskloof-dam-004",
  "@type": "resco:Entity",
  "resco:entityType": "Dam",
  "resco:hasMeasurement": {
    "@id": "resco:Measurement/theewaterskloof-dam-004",
    "@type": "resco:Measurement",
    "resco:measurementLabel": "Water Volume (liters)",
    "resco:measurementValue": 480188000000.0,
    "resco:measurementUnit": "liters",
    "resco:measurementTimestamp": "2025-09-22T05:30:00Z"
  }
}
```

**Dam Condition**

We can model the dam's condition to monitor infrastructure and schedule maintenance across the water supply system.

```json
{
  "@id": "resco:Condition/theewaterskloof-dam-004-status",
  "@type": "resco:Condition",
  "resco:conditionTag": "Water Infrastructure",
  "resco:conditionLabel": "Dam operational status",
  "resco:conditionValue": "Operational",
  "resco:conditionOptions": ["Operational", "Under Maintenance"],
  "resco:appliesTo": "Entity/theewaterskloof-dam-004"
}
```

**Dam Storage with Quantitative Indicators**

If we have a Measurement for the dam's total capacity (i.e. the total volume the dam can hold) as compared to its current level, we can generate an Indicator of the dam's current % storage.

```json
{
  "@id": "resco:Indicator/theewaterskloof-dam-004-storage",
  "@type": "resco:Indicator",
  "resco:indicatorType": "% Storage",
  "resco:indicatorValue": 86.1,
  "resco:indicatorUnit": "%",
  "resco:indicatesCondition": "resco:Condition/cape_town_water_resource_status"
}
```

With water storage readings across each dam in the water supply system, we can report on the % gross water storage across the city.

```json
{
  "@id": "resco:Indicator/cape_town_gross_water_storage",
  "@type": "resco:Indicator",
  "resco:indicatorType": "% Gross Water Storage",
  "resco:indicatorValue": 92.3,
  "resco:indicatorUnit": "%",
  "resco:basedOnMeasurement": [
    "resco:Indicator/theewaterskloof-dam-004-storage",
    "resco:Indicator/berg-river-dam-001-storage",
    "resco:Indicator/steenbras-lower-dam-002-storage",
    "resco:Indicator/steenbras-upper-dam-003-storage",
    "resco:Indicator/voëlvei-dam-005-storage",
    "resco:Indicator/alexandra-dam-007-storage",
    "resco:Indicator/de-villiers-dam-008-storage",
    "resco:Indicator/hely-hutchinson-dam-009-storage",
    "resco:Indicator/kleinplaats-dam-010-storage",
    "resco:Indicator/land-en-zeezicht-dam-011-storage",
    "resco:Indicator/lewis-gay-dam-012-storage",
    "resco:Indicator/victoria-dam-013-storage",
    "resco:Indicator/woodhead-dam-014-storage"
  ],
  "resco:indicatesCondition": "resco:Condition/cape_town_water_resource_status"
}
```

**Conditions informing City Response**

With % gross water storage across the water supply system, we can track the water resource status as a Condition, using the condition to inform city-wide decision-making on the water supply.

```json
{
  "@id": "resco:Condition/cape_town_water_resource_status",
  "@type": "resco:Condition",
  "resco:conditionLabel": "Cape Town Water Resource Status",
  "resco:conditionValue": "Wise Water Use",
  "resco:conditionOptions": [
    "Wise Water Use",
    "Early Drought Caution",
    "Drought Response",
    "Accelerated Drought Response",
    "Emergency Drought Response"
  ],
  "resco:conditionTag": "Water Resource Status",
  "resco:appliesTo": "resco:Entity/western-cape-water-supply-system",
  "resco:derivedFrom": "resco:Indicator/cape-town-gross-water-storage"
}
```

---

### 2. Cape Town Water Supply System Water Quality

**Water Quality Tests as Events**

We model each water quality as an Event. Each test involves a Measurement(s) depending on the tests required.

```json
{
  "@id": "resco:Event/water-quality-test-001001001",
  "@type": "resco:Event",
  "resco:eventType": "waterQualityTest",
  "resco:eventTime": "2025-07-222T05:30:00Z",
  "resco:generatedBy": "resco:Entity/water-quality-sensor-001",
  "resco:involvedEntity": ["resco:Entity/berg-river-dam-001"],
  "resco:hasMeasurement": [
    "resco:Measurement/water-quality-sensor-001-temperature-reading",
    "resco:Measurement/water-quality-sensor-001-ph-reading",
    "resco:Measurement/water-quality-sensor-001-dissolved-oxygen-reading",
    "resco:Measurement/water-quality-sensor-001-free-chlorine-reading",
    "resco:Measurement/water-quality-sensor-001-turbidity-reading",
    "resco:Measurement/water-quality-sensor-001-conductivity-reading",
    "resco:Measurement/water-quality-sensor-001-nitrogen-reading",
    "resco:Measurement/water-quality-sensor-001-phosphorus-reading"
  ]
}
```

**Qualitative Indicator with Water Quality Results**

We use an Indicator to aggregate the results of the tests involved, based on sensor reading Measurements across a dam in the water supply system. Measurements can also be used to model lab results. The aggregate of the readings determines whether the water quality test at this dam (Berg River) is passed.

```json
{
  "@id": "resco:Indicator/water-quality-results-dam-001",
  "@type": "resco:Indicator",
  "resco:indicatorLabel": "Berg River Water Quality Results",
  "resco:indicatorValue": "Passed",
  "resco:indicatorUnit": "",
  "resco:indicatesCondition": "Water Quality Status",
  "resco:basedOnMeasurement": [
    "resco:Measurement/water-quality-sensor-001-temperature-reading",
    "resco:Measurement/water-quality-sensor-001-ph-reading",
    "resco:Measurement/water-quality-sensor-001-dissolved-oxygen-reading",
    "resco:Measurement/water-quality-sensor-001-free-chlorine-reading",
    "resco:Measurement/water-quality-sensor-001-turbidity-reading",
    "resco:Measurement/water-quality-sensor-001-conductivity-reading",
    "resco:Measurement/water-quality-sensor-001-nitrogen-reading",
    "resco:Measurement/water-quality-sensor-001-phosphorus-reading"
  ]
}
```

**Water Quality Compliance Indicator based on pass/fail rates**

With the aggregated water quality test results from all the dams, we report on the % pass rate, which informs the water supply system's compliance results.

```json
{
  "@id": "resco:Indicator/water-quality-compliance",
  "@type": "resco:Indicator",
  "resco:indicatorLabel": "Western Cape Water Supply System Water Quality Compliance",
  "resco:indicatorValue": "99.69",
  "resco:indicatorUnit": "%",
  "resco:indicatesCondition": "Water Quality Status",
  "resco:basedOnMeasurement": [
    "resco:Indicator/water-quality-results-dam-001",
    "resco:Indicator/water-quality-results-dam-002",
    "resco:Indicator/water-quality-results-dam-003",
    "resco:Indicator/water-quality-results-dam-004",
    "resco:Indicator/water-quality-results-dam-005",
    "resco:Indicator/water-quality-results-dam-006",
    "resco:Indicator/water-quality-results-dam-007",
    "resco:Indicator/water-quality-results-dam-008",
    "resco:Indicator/water-quality-results-dam-009",
    "resco:Indicator/water-quality-results-dam-010",
    "resco:Indicator/water-quality-results-dam-011",
    "resco:Indicator/water-quality-results-dam-012",
    "resco:Indicator/water-quality-results-dam-013",
    "resco:Indicator/water-quality-results-dam-014"
  ]
}
```

**Water Quality Status**

With the water quality compliance results, we indicate a Condition of whether the water in the water supply system is safe for drinking or not. We can also show that final results are still pending when readings are still being completed across dams.

```json
{
  "@id": "resco:Condition/water-quality-status",
  "@type": "resco:Condition",
  "resco:conditionTag": "Water Quality",
  "resco:conditionLabel": "Water quality status results",
  "resco:conditionValue": "Safe",
  "resco:conditionOptions": ["Safe", "Unsafe", "Results Pending"],
  "resco:appliesTo": "Indicator/water-quality-test-results"
}
```
