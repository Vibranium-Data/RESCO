## Example: Olsztyn Real Estate Pricing

Domain: Real Estate, Urban Planning

Data Source: [Poland Open Data Datasets](https://dane.gov.pl/en/dataset/5244)

Olsztyn is a smart city project located in Poland. As community development continues, we look at how urban practitioners, including city management, can analyze and make available real estate prices for construction projects as offers for a variety of projects are received. This aids with infrastructure investment planning and price transparency for city management while enabling real estate investors and developers to better understand price trends and project availability.

**Real Estate Projects as Entities**

We first model each real estate project as an Entity of entityType Asset. We can also model each component within the overall project, for example a unit, as Entities as well. This enables us to get project-level and unit-level views for the project, and to differentiate between different components in the overall project.

```json
{
  "@context": {
    "resco": "http://github.com/vibranium-data/resco",
    "schema": "http://schema.org#"
  },
    {
      "@id": "resco:Entity/re_project_0000001",
      "@type": "resco:Entity",
      "resco:entityId": "re_project_0000001",
      "resco:entityName": "Apartment Blocks - Sokola Street",
      "resco:entityType": "Asset",
      "resco:entityTag": ["EKOBUD pbo", "housing", "olsztyn"],
      "resco:hasCondition": "resco:Condition/real-estate-project-status"
    }
}

```
