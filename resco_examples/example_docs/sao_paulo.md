## Example: Sao Paulo and Rio de Janeiro Energy - Grid Supply and Demand

Domain: Energy

Data source: [IPDO-ONS Balance of Energy Reports](https://www.ons.org.br/paginas/energia-agora/carga-e-geracao)

You can find the archived data source for the example [here](../data_sources/brazil_IPDO-22-09-2025.pdf).

### 1. Sao Paulo and Rio de Janeiro Grid Energy Supply

**Power Plant as Entity**

Each power is modeled as an Entity. Here, we have each dam associated with an energy reading, read by the power plant's meters. We can either model the power plant's meters granularly, meter by meter, or the power plant overall and its associated total capacity. We can have different types of entities - from organizations, systems composed of different machines, to even individual actors, so we use the entityType label to show that we are modeling a Power Plant. Sao Paulo and Rio de Janeiro get power from varying energy sources - hydropower, oil and gas, nuclear, bioenergy, solar and wind, so we use the entityTag to label the type of power plant. We also add an entityTag for the grid subsystem that Sao Paulo and Rio de Janeiro are a part of. The data source reports the energy supplied by each power plant in megawatts (MW), so we use that for the Measurement.

```json
{
  "@context": {
    "resco": "https://www.github.com/vibranium-data/resco",
    "schema": "http://schema.org/"
  },
  "@id": "resco:Entity/angra-ii-005",
  "@type": "resco:Entity",
  "resco:entityType": "Power Plant",
  "resco:entityTag": ["Nuclear", "Sudeste / Centro-Oeste"],
  "resco:hasMeasurement": {
    "@id": "resco:Measurement/angra-ii-002-available-power",
    "@type": "resco:Measurement",
    "resco:measurementLabel": "Available Power Capacity (MW)",
    "resco:measurementValue": 1350.0,
    "resco:measurementUnit": "megawatts",
    "resco:measurementTimestamp": "2025-09-22T05:00:00Z"
  }
}
```

We can also have a Measurement of the installed power capacity, which is the power capacity the plant was installed to produce (vs what is actually made available).

```json
{
  "@id": "resco:Measurement/angra-ii-002-installed-power",
  "@type": "resco:Measurement",
  "resco:measurementLabel": "Installed Power Capacity (MW)",
  "resco:measurementValue": 1350.0,
  "resco:measurementUnit": "megawatts",
  "resco:measurementTimestamp": "2025-09-22T05:00:00Z"
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

**Grid Supply with Quantitative Indicators**

If we have a Measurement for the power plant's daily energy supply, say taken by plant meters hour by hour, we can aggregate these hourly meter readings to generate a daily average energy supply Indicator. We can model the verified daily average energy supply for Angra II power plant as shown in the data source in RESCO as shown below.

```json
{
  "@id": "resco:Indicator/angra-ii-005-verified-daily-avg-power-supply",
  "@type": "resco:Indicator",
  "resco:indicatorType": "Average Power Supply, Daily Verified",
  "resco:indicatorValue": 1361.0,
  "resco:indicatorUnit": "MW",
  "resco:indicatesCondition": "resco:Condition/angra-ii-005-daily-avg-power-supply-SLA"
}
```

We can also model the scheduled or expected daily average, according to either SLAs or targets set by ONS, or the power plant's Engineering division.

```json
{
  "@id": "resco:Indicator/angra-ii-005-scheduled-daily-avg-power-supply",
  "@type": "resco:Indicator",
  "resco:indicatorType": "Average Power Supply, Daily Scheduled",
  "resco:indicatorValue": 1350.0,
  "resco:indicatorUnit": "MW",
  "resco:indicatesCondition": "resco:Condition/angra-ii-005-daily-avg-power-supply-SLA"
}
```

We can use these two Indicators to model another Indicator which tells us by how much the scheduled vs verified power supply varied, either in raw (absolute) values or in percentage, as shown in the data source.
Average vs Verified power supply in absolute values

```json
{
  "@id": "resco:Indicator/angra-ii-005-avg-daily-power-supply-scheduled-vs-verified",
  "@type": "resco:Indicator",
  "resco:indicatorType": "Average Power Supply, Daily Scheduled vs Verified",
  "resco:indicatorValue": 11,
  "resco:indicatorUnit": "MW",
  "resco:indicatesCondition": "resco:Condition/angra-ii-005-daily-avg-power-supply-SLA"
}
```

Average vs Verified power supply in percentage

```json
{
  "@id": "resco:Indicator/angra-ii-005-avg-daily-power-supply-scheduled-vs-verified",
  "@type": "resco:Indicator",
  "resco:indicatorType": "Average Power Supply, Daily Scheduled vs Verified",
  "resco:indicatorValue": 1.0,
  "resco:indicatorUnit": "%",
  "resco:indicatesCondition": "resco:Condition/angra-ii-005-daily-avg-power-supply-SLA"
}
```

**Aggregating Indicators**

We can extend similar Measurements and Indicators to every power plant supplying Sao Paulo and Rio de Janeiro, representing each power plant as an Entity. We can then measure the verified average daily power supply across the entire grid, versus what was scheduled. Both Sao Paulo and Rio de Janeiro are supplied by the Sudeste / Centro-Oeste subsystem of Brazil's grid. We can group by the entityTag we used for the grid subsystem to easily get the desired power plants. Aggregating the Measurements and Indicators across the Sudeste / Centro-Oeste part of the grid to get these daily average power supply metrics in RESCO would look like this:

```json
{
  "@id": "resco:Indicator/sudeste-centro-oeste-verified-avg-daily-power-supply",
  "@type": "resco:Indicator",
  "resco:indicatorType": "Grid Average Power Supply, Daily Verified",
  "resco:indicatorValue": 5699,
  "resco:indicatorUnit": "MW",
  "resco:basedOnMeasurement": [
    "resco:Indicator/do-atlantico-001-verified-daily-avg-power-supply",
    "resco:Indicator/w-arjona-002-verified-daily-avg-power-supply",
    "resco:Indicator/daio-003-verified-daily-avg-power-supply",
    "resco:Indicator/xavantes-004-verified-daily-avg-power-supply",
    "resco:Indicator/angra-ii-005-verified-daily-avg-power-supply",
    "resco:Indicator/angra-i-006-verified-daily-avg-power-supply",
    "resco:Indicator/marlim-azul-007-verified-daily-avg-power-supply",
    "resco:Indicator/baixada-fluminense-008-verified-daily-avg-power-supply",
    "resco:Indicator/santa-cruz-nova-009-verified-daily-avg-power-supply",
    "resco:Indicator/luiz-melo-010-verified-daily-avg-power-supply",
    "resco:Indicator/gna-i-011-verified-daily-avg-power-supply",
    "resco:Indicator/cubatao-012-verified-daily-avg-power-supply",
    "resco:Indicator/gna-ii-013-verified-daily-avg-power-supply",
    "resco:Indicator/karkey-013-013-verified-daily-avg-power-supply",
    "resco:Indicator/karkey-019-014-verified-daily-avg-power-supply",
    "resco:Indicator/tres-lagoas-015-verified-daily-avg-power-supply",
    "resco:Indicator/porsud-i-016-verified-daily-avg-power-supply",
    "resco:Indicator/porsud-ii-017-verified-daily-avg-power-supply",
    "resco:Indicator/termomacae-018-verified-daily-avg-power-supply",
    "resco:Indicator/cuiaba-019-verified-daily-avg-power-supply",
    "resco:Indicator/ibirite-020-verified-daily-avg-power-supply",
    "resco:Indicator/termorio-021-verified-daily-avg-power-supply",
    "resco:Indicator/norte-fluminese-022-verified-daily-avg-power-supply",
    "resco:Indicator/viana-023-verified-daily-avg-power-supply",
    "resco:Indicator/povocao-1-024-verified-daily-avg-power-supply",
    "resco:Indicator/viana-1-025-verified-daily-avg-power-supply",
    "resco:Indicator/seropedica-026-verified-daily-avg-power-supply",
    "resco:Indicator/juiz-de-fora-027-verified-daily-avg-power-supply",
    "resco:Indicator/nova-piratininga-028-verified-daily-avg-power-supply",
    "resco:Indicator/palmeiras-de-goias-029-verified-daily-avg-power-supply"
  ],
  "resco:indicatesCondition": "resco:Condition/sudeste_centro_oeste_daily-avg-power-supply-SLA"
}
```

Upon similarly aggregating the average daily scheduled power supply, we can also then aggregate indicators for the Scheduled vs Verified Average Daily Power Supply for the entire grid subsystem for the Sudeste Centro Oeste region. This could then inform a Condition for the service-level agreements (SLAs) at the utility, city or region level on whether the grid subsystem is supplying the expected power. If this is not the case, it would be possible to identify which power plants need improvement, perhaps for maintenance or even checking whether their meters are in good condition and reporting the correct values.

**Conditions informing City, Utility or Organization Response**

With verified daily average power supply across the region's grid, we can track the daily power supply service level agreement (SLA) as a Condition, using the condition to inform decision-making at the regional level, or within a city, utility or other organization for the grid's power supply.

```json
{
  "@id": "resco:Condition/sudeste_centro_oeste_daily-avg-power-supply-SLA",
  "@type": "resco:Condition",
  "resco:conditionLabel": "Sudeste/Centro-Oeste Daily Power Supply SLA",
  "resco:conditionValue": "Power Supply Quality, Daily Average SLA",
  "resco:conditionOptions": [
    "Power Supply Agreement Met - Above Expectations",
    "Power Supply Agreement Met - Standard",
    "Power Supply Agreement Unmet",
    "Power Supply Agreement Unmet - Exploration Recommended"
  ],
  "resco:conditionTag": "Daily Power Supply SLA",
  "resco:appliesTo": "resco:Entity/sudeste_centro_oeste_grid-system",
  "resco:derivedFrom": "resco:Indicator/sudeste-centro-oeste-avg-daily-power-supply-scheduled-vs-verified"
}
```

**Energy Transmission as Events**

As the grid gets different requests for energy as people turn appliances on and off, these can be modeled as Events, associated with a utility user, such as a household or factory with an account within a utility. Here, the load request to the grid is shown to be from the utility Enel Distribuição São Paulo. We can have more than one involvedEntity during an Event. Here, we show both the grid in Sao Paulo specifically and the regional grid used in ONS data.

```json
{
  "@id": "resco:Event/load-request-2025-09-22",
  "@type": "resco:Event",
  "resco:eventType": "load request",
  "resco:eventTime": "2025-09-22T10:30:00Z",
  "resco:involvedEntity": [
    "resco:Entity/sao-paulo-grid",
    "resco:Entity/sudeste_centro_oeste_grid-system"
  ],
  "resco:generatedBy": "resco:Entity/enel-sao-paulo-004-005"
}
```

We can log these load requests and over the course of the day, aggregate them across the grid. We can then model the moment during the day when peak demand occurred across the grid as an Event. An example of a peak demand event can be as follows:

```json
{
  "@id": "resco:Event/peak-demand-2025-09-22",
  "@type": "resco:Event",
  "resco:eventType": "PeakDemand",
  "resco:eventTime": "2025-09-22T10:46:00Z",
  "resco:involvedEntity": [
    "resco:Entity/sudeste_centro_oeste_grid-system",
    "resco:Entity/ONS"
  ],
  "resco:generatedBy": "resco:Entity/sudeste_centro_oeste_grid-system"
}
```

Alternatively, we can also model peak demand as a Measurement and generate its associated Indicator.

```json
{
  "@id": "resco:Measurement/sudeste-centro-oeste-grid-demand-2025-09-22",
  "@type": "resco:Measurement",
  "resco:measurementLabel": "Grid Demand Sudeste Centro Oeste (MW)",
  "resco:measurementValue": 51.896,
  "resco:measurementUnit": "megawatts",
  "resco:measurementTimestamp": "2025-09-22T10:30:00Z"
}
```

```json
{
  "@id": "resco:Indicator/sudeste-centro-oeste-peak-demand-2025-09-22",
  "@type": "resco:Indicator",
  "resco:indicatorType": "Peak Demand Sudeste Centro Oeste (MW)",
  "resco:indicatorValue": 53.714,
  "resco:indicatorUnit": "MW"
}
```

**Grid Stability Status**

We can model grid supply and grid demand as Measurements.

```json
{
  "@id": "resco:Measurement/sudeste-centro-oeste-grid-demand-2025-09-22",
  "@type": "resco:Measurement",
  "resco:measurementLabel": "Grid Demand Sudeste Centro Oeste (MW)",
  "resco:measurementValue": 51.896,
  "resco:measurementUnit": "megawatts",
  "resco:measurementTimestamp": "2025-09-22T10:30:00Z"
}
```

```json
{
  "@id": "resco:Measurement/sudeste-centro-oeste-grid-supply-2025-09-22",
  "@type": "resco:Measurement",
  "resco:measurementLabel": "Grid Supply Sudeste Centro Oeste (MW)",
  "resco:measurementValue": 235.213,
  "resco:measurementUnit": "megawatts",
  "resco:measurementTimestamp": "2025-09-22T10:30:00Z"
}
```

Using these measurements for grid supply and grid demand, we can generate an Indicator that reports whether the grid's supply and demand are balanced, which informs us about grid stability.

```json
{
  "@id": "resco:Indicator/sudeste-centro-oeste-grid-balance-2025-09-22",
  "@type": "resco:Indicator",
  "resco:indicatorLabel": "Grid Supply–Demand Balance Sudeste Centro Oeste (MW)",
  "resco:indicatorValue": 183.317,
  "resco:indicatorUnit": "MW",
  "resco:basedOnMeasurement": [
    "resco:Measurement/sudeste-centro-oeste-grid-demand-2025-09-22",
    "resco:Measurement/sudeste-centro-oeste-grid-supply-2025-09-22"
  ],
  "resco:indicatesCondition": "resco:Condition/sudeste-centro-oeste-grid-stability"
}
```

We can then use the grid balance Indicator to generate a Condition which informs ONS, utilities and city leadership about grid stability in the region.

```json
{
  "@id": "resco:Condition/sudeste-centro-oeste-grid-stability",
  "@type": "resco:Condition",
  "resco:conditionLabel": "Grid equilibrium",
  "resco:conditionValue": "Stable"
}
```

**Interventions to Stabilize Grid Load**

Depending on peak demand across the grid, operators might need to take actions to improve grid stability. We can model these actions as Interventions. Examples of Interventions in this case could include increasing hydro discharge at a hydroelectric plant, rerouting imports from another subsystem, activating inactive thermal plants to meet demand peaks, or other Interventions as needed.

We model an Intervention to increase the hydro discharge below, until power generation reaches 9600 MW at the specified plant.

```json
{
  "@id": "resco:Intervention/hydro-discharge-adjustment",
  "@type": "resco:Intervention",
  "resco:interventionLabel": "Hydroelectric dispatch adjustment",
  "resco:implementedBy": "resco:Entity/ONS",
  "resco:appliesTo": "resco:Entity/itaipu-plant",
  "resco:basedOnIndicator": "resco:Indicator/sudeste-centro-oeste-peak-demand-2025-09-22",
  "resco:currentEntityCondition": "resco:Condition/hydro-low-reservoir",
  "resco:targetEntityCondition": "resco:Condition/hydro-normal-reservoir",
  "resco:interventionStartTime": "2025-09-22T19:10:00Z",
  "resco:interventionEndTime": "2025-09-22T20:00:00Z",
  "resco:interventionOutcome": "Generation increased to 9600 MW"
}
```

Here's another example of an Intervention, this time to reroute transmission from the Southeast / Central region where Sao Paulo is located to the national grid (National Interconnected System) for redistribution to the North East subregion.

```json
{
  "@id": "resco:Intervention/transmission-rerouting-southeast",
  "@type": "resco:Intervention",
  "resco:interventionLabel": "Transmission rerouting to balance regional load",
  "resco:implementedBy": "resco:Entity/ONS",
  "resco:appliesTo": "resco:Entity/sudeste-centro-oeste-grid-system",
  "resco:basedOnIndicator": "resco:Indicator/sudeste-centro-oeste-grid-balance-2025-09-22",
  "resco:currentEntityCondition": "resco:Condition/nordeste-grid-balance-overload",
  "resco:targetEntityCondition": "resco:Condition/northeast-demand-balanced",
  "resco:interventionStartTime": "2025-09-22T21:00:00Z",
  "resco:interventionEndTime": "2025-09-22T22:00:00Z",
  "resco:interventionOutcome": "Excess generation of 100 MW rerouted from Southeast subsystem to Northeast subsystem via NIS Interconnection 2."
}
```

---

## Example: Sao Paulo Air Quality

Domain: Climate / Environment

Data source: [AQICN Air Quality Data](https://aqicn.org/network/cetesb/)

**Sensors as Entities**
We model the air quality sensors in Sao Paulo's to generate PM10 air quality measurements at each station.
Sensors are treated as Entities with entityType as _"Sensor"_ that generate Measurements.

```json
{
  "@context": {
    "resco": "https://github.com/vibranium-data/resco",
    "schema": "http://schema.org/"
  },
  "@id": "resco:Entity/sao-paulo-sensor-000002243",
  "@type": "resco:Entity",
  "resco:entityType": "AirQualitySensor",
  "resco:hasMeasurement": {
    "@id": "resco:Measurement/nbo-cbd-sensor-000002243-pm10",
    "@type": "resco:Measurement",
    "resco:measurementLabel": "PM10 concentration (µg/m³)",
    "resco:measurementValue": 23.0,
    "resco:measurementUnit": "µg/m³",
    "resco:measurementTimestamp": "2025-10-14T13:00:00Z"
  }
}
```

**Infrastructure Condition in RESCO (JSON-LD)**

We can monitor the Condition of each sensor to ensure readings are coming from operational sensors and to schedule maintenance as needed.

```json
{
  "@id": "resco:Condition/sao-paulo-sensor-000002243-status",
  "@type": "resco:Condition",
  "resco:conditionTag": "air quality infrastructure",
  "resco:conditionLabel": "Sensor operational status",
  "resco:conditionValue": "Operational",
  "resco:conditionOptions": [
    "Operational",
    "Under Maintenance",
    "Not Responding",
    "Offline"
  ]
}
```

**Indicator Representation in RESCO (JSON-LD)**

We aggregate the air quality measurements from every sensor in the Sao Paulo to generate an Air Quality Index for the entire city. We can also compare air quality metrics across different regions in the city.

Here, we show an example of modelling an Air Quality Index for Sao Paulo by aggregating Measurements from five sensors.

```json
{
  "@id": "resco:Indicator/sao-paulo-pm10-aqi",
  "@type": "resco:Indicator",
  "resco:indicatorType": "AirQualityIndex",
  "resco:indicatorValue": 61,
  "rescoindicatorUnit": "AQI",
  "resco:indicatesCondition": "resco:Condition/sao-paulo-pm10-quality",
  "resco:basedOnMeasurement": [
    "resco:resco:Measurement/sao-paulo-sensor-000002243-pm10",
    "resco:resco:Measurement/sao-paulo-sensor-000002244-pm10",
    "resco:resco:Measurement/sao-paulo-sensor-000002245-pm10",
    "resco:resco:Measurement/sao-paulo-sensor-000002246-pm10",
    "resco:resco:Measurement/sao-paulo-sensor-000002247-pm10"
  ]
}
```

**Environmental Condition in RESCO (JSON-LD)**

We can then model a Condition for the air quality in Sao Paulo for continuous monitoring, evaluation and reporting across the city.

```json
{
  "@id": "resco:Condition/sao-paulo-pm10-quality",
  "@type": "resco:Condition",
  "resco:conditionTag": "environment",
  "resco:conditionLabel": "Air Quality Condition",
  "resco:conditionOptions": "['Good', 'Moderate', 'Poor']",
  "resco:conditionValue": "Moderate"
}
```
