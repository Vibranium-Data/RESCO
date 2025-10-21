## Example: Olsztyn Real Estate Pricing

Domain: Real Estate, Urban Planning

Data Source: [Poland Open Data Datasets](https://dane.gov.pl/en/dataset/5244)

Olsztyn is a smart city project located in Poland. As community development continues, we look at how urban practitioners, including city management, can analyze and make available real estate prices for construction projects as offers for a variety of projects are received. This aids with infrastructure investment planning and price transparency for city management while enabling real estate investors and developers to better understand price trends and project availability.

**Real Estate Projects as Entities**

We first model each real estate project as an Entity of entityType Asset. We can also model each component within the overall project, for example a unit, as Entities as well. This enables us to get project-level and unit-level views for the project, and to differentiate between different components in the overall project.

First, we model an overall real estate project for apartment blocks on Sokola Street:

```json
{
  "@context": {
    "resco": "http://github.com/vibranium-data/resco",
    "schema": "http://schema.org#"
  },
    {
      "@id": "resco:Entity/re_project_sokola_pr00001",
      "@type": "resco:Entity",
      "resco:entityId": "re_project_sokola_pr00001",
      "resco:entityName": "Apartment Blocks - Sokola Street",
      "resco:entityType": "Asset",
      "resco:entityTag": ["EKOBUD pbo", "housing", "olsztyn"],
      "resco:hasMeasurement":"resco:Measurement/re_project_sokola_pr00001_price",
      "resco:hasCondition": "resco:Condition/real-estate-project-status"
    }
}

```

We can then model each apartment unit for this particular project, including both Conditions for the overall real estate project and those specifically for the unit to enable project tracking at the unit or project level.

```json
{
  "@id": "resco:Entity/re_project_sokola_pu00001",
  "@type": "resco:Entity",
  "resco:entityId": "re_project_sokola_pu00001",
  "resco:entityName": "Apartment Unit, Apartment Blocks - Sokola Street",
  "resco:entityType": "Asset",
  "resco:hasMeasurement": "resco:Measurement/re_project_pu00001_price",
  "resco:entityTag": ["EKOBUD pbo", "housing", "olsztyn"],
  "resco:hasCondition": [
    "resco:Condition/real-estate-project-status",
    "resco:Condition/real-estate-unit-status"
  ]
}
```

**Real Estate Prices as Measurements and Indicators**

We can use Measurements to model real estate prices both at the project and unit level. We can use the generatedBy property in RESCO's Measurement class to show who is reporting or updating the price. An example from our dataset involving an offer price at the unit level for EKOBUD PBO for apartment blocks on Sokola Street would look like this:

```json
{
  "@id": "resco:Measurement/re_project_sokola_pu00001_price",
  "@type": "resco:Measurement",
  "resco:measurementId": "re_project_sokola_pu00001_price",
  "resco:measurementLabel": "Relative Humidity",
  "resco:measurementValue": 347802.0,
  "resco:measurementUnit": "PLN",
  "resco:measurementTime": "2025-10-20T09:00:00Z",
  "resco:generatedBy": "resco:Entity/ekobud-pbo-2001"
}
```

The real estate project might involve different prices for each unit depending on floor area, bedrooms or amenities. The project might also involve other spaces such as parking whose price may not be included in the per-unit price. To get an estimate for an entire project composed of different types of units, we can create an Indicator for the project's total price or total investment. For example, let's consider if the above project on Sokola street had 12 different units each costing 348,702.00 PLN as well as basement parking costing 700,000 PLN. Here's how we would model the entire project's price in RESCO:

```json
{
  "@id": "resco:Indicator/re_project_sokola_pr00001_price",
  "@type": "resco:Indicator",
  "resco:indicatorLabel": "Project Price Apartment Blocks - Sokola Street",
  "resco:indicatorValue": "4884424.00",
  "resco:indicatorUnit": "PLN",
  "resco:basedOnMeasurement": [
    "resco:Measurement/re_project_sokola_pu00001_price",
    "resco:Measurement/re_project_sokola_pu00002_price",
    "resco:Measurement/re_project_sokola_pu00003_price",
    "resco:Measurement/re_project_sokola_pu00004_price",
    "resco:Measurement/re_project_sokola_pu00005_price",
    "resco:Measurement/re_project_sokola_pu00006_price",
    "resco:Measurement/re_project_sokola_pu00007_price",
    "resco:Measurement/re_project_sokola_pu00008_price",
    "resco:Measurement/re_project_sokola_pu00009_price",
    "resco:Measurement/re_project_sokola_pu00010_price",
    "resco:Measurement/re_project_sokola_pu00011_price",
    "resco:Measurement/re_project_sokola_pu00012_price",
    "resco:Measurement/re_project_pr_sokola_parking_price"
  ]
}
```

**Project Status with Conditions**

We can use Conditions to track the each project or unit's status as the phases of construction progress. We can even use Conditions to show whether the project was delivered within the budget.

```json
{
  "@id": "resco:Condition/real-estate-project-status",
  "@type": "resco:Condition",
  "resco:conditionLabel": "Real Estate Project Overall Status",
  "resco:conditionTag": ["real estate project" "olsztyn", "construction phases"],
  "resco:conditionValue": "Planning",
  "resco:conditionOptions": ["Bid Evaluation", "Developer Selected", "Planning", "In Construction", "Construction Complete", "Announced for Occupancy", "Active Occupancy"],
  "resco:appliesTo": "resco:Entity/re_project_sokola_pr00001"
}
```

```json
{
  "@id": "resco:Condition/real-estate-project-budget-status",
  "@type": "resco:Condition",
  "resco:conditionLabel": "Real Estate Project Budget Status",
  "resco:conditionTag": ["real estate project" "olsztyn", "construction phases"],
  "resco:conditionValue": "Within Budget",
  "resco:conditionOptions": ["Within Budget", "Over Budget"],
  "resco:appliesTo": "resco:Entity/re_project_sokola_pr00001"
}
```

We can also have more granular Conditions at the unit level that help with tracking the progress of construction with details reported by the real estate developer. Here's an example for one of the apartment block units for the project on Sokola Street:

```json
{
  "@id": "resco:Condition/real-estate-project-construction-status",
  "@type": "resco:Condition",
  "resco:conditionLabel": "Real Estate Project Construction Status",
  "resco:conditionTag": ["real estate project" "sokola street", "construction phases"],
  "resco:conditionValue": "Planning",
  "resco:conditionOptions": ["Planning", "Plans Pending Approval", "Plans Approved", "Funds Released", "Construction Ongoing", "Structure Complete - Pending Finishes", "Structure and Finishes Complete", "Construction Complete - Pending Inspection", "Construction and Inspection Complete", "Construction Complete - Announced for Occupancy", "Construction Complete - Active Occupancy"],
  "resco:appliesTo": "resco:Entity/re_project_sokola_pu00001"
}
```
