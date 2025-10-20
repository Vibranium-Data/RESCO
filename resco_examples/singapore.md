## Example: Singapore - Weather Conditions

Domain: Climate

Data source: [Singapore Real Time Weather Readings Datasets](https://data.gov.sg/collections/1459/view)

### 1. Singapore Instruments and Readings from Weather Stations

We can model weather condition data from readings in various weather stations across Singapore. Singapore has various weather readings datasets available, including data on air temperature, rainfall, relative humidity, wind direction and wind speed. For our modeling examples, we'll explore modeling air temperature and humidity data.

**Weather Stations and Thermometers as Entities**

We can model each weather station across Singapore as an Entity of entityType weather station. We can also model the thermometer at the weather station as an Entity of entityType Sensor. Alternatively, we can be even more specific and add the entityType as Thermometer. In this example, we'll add thermometer as an entityTag.

```json
{
  "@context": {
    "resco": "http://github.com/vibranium-data/resco",
    "schema": "http://schema.org#"
  },
    {
      "@id": "resco:Entity/S108",
      "@type": "resco:Entity",
      "resco:entityId": "S108",
      "resco:entityName": "Marina Gardens Drive Weather Station",
      "resco:entityType": "WeatherStation",
      "resco:entityTag": ["weather", "marina gardens", "singapore"],
      "resco:hasCondition": "resco:Condition/operational"
    }
}

```

```json
{
  "@id": "resco:Entity/S108",
  "@type": "resco:Entity",
  "resco:entityId": "thermometer-S108",
  "resco:entityName": "Thermometer - Marina Gardens Drive Weather Station",
  "resco:entityType": "Sensor",
  "resco:entityTag": ["thermometer", "temperature", "singapore"],
  "resco:hasCondition": "resco:Condition/operational"
}
```

**Thermometer Condition in RESCO (JSON-LD)**

```json
{
  "@id": "resco:Condition/operational",
  "@type": "resco:Condition",
  "resco:conditionId": "operational",
  "resco:conditionLabel": "Operational",
  "resco:conditionOptions": [
    "Operational",
    "Under Maintenance",
    "Not Responding",
    "Offline"
  ],
  "resco:appliesTo": "resco:Entity/thermometer-S108"
}
```

**Temperature Readings as Measurements**

We can then model the temperature reading from the thermometer at the weather station as a Measurement.

```json
{
  "@id": "resco:Measurement/S108-temp-2024-07-16T15:59:00Z",
  "@type": "resco:Measurement",
  "resco:measurementId": "S108-temp-2024-07-16T15:59:00Z",
  "resco:measurementLabel": "Air Temperature",
  "resco:measurementValue": 29,
  "resco:measurementUnit": "°C",
  "resco:measurementTime": "2024-07-16T15:59:00Z",
  "resco:generatedBy": "resco:Entity/thermometer-S108"
}
```

**Relative Humidity in RESCO**
Here's another example of a weather reading in RESCO, this time of humidity measured in Singapore.
You can find the Singapore weather data from their open data [here](https://data.gov.sg/datasets/d_2d3b0c4da128a9a59efca806441e1429/view).

**Weather Station and Humidity Sensors as Entities**

We again model each weather station as an Entity, along with each humidity sensor. We use the entityType property to specify the type of entity, and entityTag properties to include additional labels relevant to practitioners, researchers or administrators.
We also expand RESCO to include an entityLocation property for the weather station, showing RESCO's easy customizability.

```json
{
  "@context": {
    "resco": "http://github.com/vibranium-data/resco",
    "schema": "http://schema.org/"
  },
    {
      "@id": "resco:Entity/S108",
      "@type": "resco:Entity",
      "resco:entityId": "S109",
      "resco:entityName": "Ang Mo Kio Avenue 5 Weather Station",
      "resco:entityType": "WeatherStation",
      "resco:entityLocation": {"lat":"1.3764","long":"103.8492"},
      "resco:entityTag": ["weather", "ang mo kio", "singapore"],
      "resco:hasCondition": "resco:Condition/operational"
    }
}

```

```json
{
  "@id": "resco:Entity/S109",
  "@type": "resco:Entity",
  "resco:entityId": "humidity-sensor-S109",
  "resco:entityName": "Hygrometer - Marina Gardens Drive Weather Station",
  "resco:entityType": "Sensor",
  "resco:entityTag": ["hygrometer", "humidity", "singapore"],
  "resco:hasCondition": "resco:Condition/operational"
}
```

**Hygrometer (Humidity Sensor) Condition in RESCO (JSON-LD)**

```json
{
  "@id": "resco:Condition/operational",
  "@type": "resco:Condition",
  "resco:conditionId": "operational",
  "resco:conditionLabel": "Operational",
  "resco:conditionOptions": [
    "Operational",
    "Under Maintenance",
    "Not Responding",
    "Offline"
  ],
  "resco:appliesTo": "resco:Entity/humidity-sensor-S109"
}
```

**Relative Humidity Readings as Measurements**

We can then model the relative humidity reading from the thermometer at the weather station as a Measurement.

```json
{
  "@id": "resco:Measurement/S109-rh-2025-10-19T01:59:00Z",
  "@type": "resco:Measurement",
  "resco:measurementId": "S109-rh-2025-10-19T01:59:00Z",
  "resco:measurementLabel": "Relative Humidity",
  "resco:measurementValue": 83.6,
  "resco:measurementUnit": "%",
  "resco:measurementTime": "2025-10-19T01:59:00Z",
  "resco:generatedBy": "resco:Entity/thermometer-S108"
}
```

**Average Relative Humidity as an Indicator**

With relative humidity Measurements across Singapore from each weather station, we can aggregate these Measurements to generate an Indicator for the average humidity across Singapore.

```json
{
  "@id": "resco:Indicator/singapore_average_humidity",
  "@type": "resco:Indicator",
  "resco:indicatorType": "Singapore Average Relative Humidity",
  "resco:indicatorValue": 83.7,
  "resco:indicatorUnit": "%",
  "resco:basedOnMeasurement": [
    "resco:Measurement/S109-rh-2025-10-19T01:59:00Z",
    "resco:Measurement/S106-rh-2025-10-19T01:59:00Z",
    "resco:Measurement/S107-rh-2025-10-19T01:59:00Z",
    "resco:Measurement/S115-rh-2025-10-19T01:59:00Z",
    "resco:Measurement/S102-rh-2025-10-19T01:59:00Z",
    "resco:Measurement/S060-rh-2025-10-19T01:59:00Z",
    "resco:Measurement/S050-rh-2025-10-19T01:59:00Z",
    "resco:Measurement/S044-rh-2025-10-19T01:59:00Z",
    "resco:Measurement/S043-rh-2025-10-19T01:59:00Z",
    "resco:Measurement/S024-rh-2025-10-19T01:59:00Z",
    "resco:Measurement/S006-rh-2025-10-19T01:59:00Z",
    "resco:Measurement/S111-rh-2025-10-19T01:59:00Z"
  ]
}
```

---

## Example 2 - Traffic Images in RESCO

Domain: Mobility, Security

We can model traffic images taken from traffic cameras across Singapore's highway networks to analyze traffic patterns, to aid with emergency response initiatives and to aid in security measures.
Data is provided by Singapore's Land Transport Authority. You can find the data [here](https://data.gov.sg/datasets/d_6cdb6b405b25aaaacbaf7689bcc6fae0/view).

**Cameras as Entities**

We model each camera as an Entity of entityType Sensor.

```json
{
  "@context": {
    "resco": "http://github.com/vibranium-data/resco",
    "schema": "http://schema.org/"
  },
    {
      "@id": "resco:Entity/C1001",
      "@type": "resco:Entity",
      "resco:entityId": "C1001",
      "resco:entityName": "traffic_camera_1001",
      "resco:entityType": "Sensor",
      "resco:entityLocation": {"lat":"1.29531332","long":"103.871146"},
      "resco:entityTag": ["camera", "traffic", "singapore"],
      "resco:hasCondition": "resco:Condition/operational"
    }
}

```

{
"items": [
{
"timestamp": "2025-10-20T12:27:45+08:00",
"cameras": [
{
"timestamp": "2025-10-20T12:26:05+08:00",
"image": "https://images.data.gov.sg/api/traffic-images/2025/10/1e12ec16-3c48-47bb-b687-97235853401d.jpg",
"location": {
"latitude": 1.29531332,
"longitude": 103.871146
},
"camera_id": "1001",
"image_metadata": {
"height": 240,
"width": 320,
"md5": "9b260b5b542f7f254bd39d52500d42bf"
}
},
{
"timestamp": "2025-10-20T12:26:05+08:00",
"image": "https://images.data.gov.sg/api/traffic-images/2025/10/50b7312b-1f15-4d7b-9eab-808dc83cb402.jpg",
"location": {
"latitude": 1.319541067,
"longitude": 103.8785627
},
"camera_id": "1002",
"image_metadata": {
"height": 240,
"width": 320,
"md5": "2efcf9e5539528df6eec8d964bfc6c1f"
}
},
{
"timestamp": "2025-10-20T12:26:05+08:00",
"image": "https://images.data.gov.sg/api/traffic-images/2025/10/0e862fc0-df37-4a60-b5d0-5458c1b109f4.jpg",
"location": {
"latitude": 1.323957439,
"longitude": 103.8728576
},
"camera_id": "1003",
"image_metadata": {
"height": 240,
"width": 320,
"md5": "74486286aa056789bf3bbd6cfabcb07f"
}
},
{
"timestamp": "2025-10-20T12:26:05+08:00",
"image": "https://images.data.gov.sg/api/traffic-images/2025/10/12c827ea-1acd-4271-8ce9-294bb7e080f1.jpg",
"location": {
"latitude": 1.319535712,
"longitude": 103.8750668
},
"camera_id": "1004",
"image_metadata": {
"height": 240,
"width": 320,
"md5": "18bb9e32e89aec6fe08ddae098c59091"
}
},
{
"timestamp": "2025-10-20T12:26:05+08:00",
"image": "https://images.data.gov.sg/api/traffic-images/2025/10/d803e3a4-341e-4a5d-868a-d0c1a3154878.jpg",
"location": {
"latitude": 1.363519886,
"longitude": 103.905394
},
"camera_id": "1005",
"image_metadata": {
"height": 240,
"width": 320,
"md5": "b1ef813ab0f41fcc0aa4f35d238ef24d"
}
},
{
"timestamp": "2025-10-20T12:26:05+08:00",
"image": "https://images.data.gov.sg/api/traffic-images/2025/10/f2ae9ef0-3e43-4981-98d3-bdc838e9398a.jpg",
"location": {
"latitude": 1.357098686,
"longitude": 103.902042
},
"camera_id": "1006",
"image_metadata": {
"height": 240,
"width": 320,
"md5": "eb17fd40e8e923d644b374caeabbb7a4"
}
},
{
"timestamp": "2025-10-20T12:26:05+08:00",
"image": "https://images.data.gov.sg/api/traffic-images/2025/10/60ede7dc-226a-45ad-ba58-4e864a3574d2.jpg",
"location": {
"latitude": 1.365434,
"longitude": 103.953997
},
"camera_id": "1111",
"image_metadata": {
"height": 1080,
"width": 1920,
"md5": "4f1bb07ed04a980dec415753c96fa76e"
}
},
{
"timestamp": "2025-10-20T12:26:05+08:00",
"image": "https://images.data.gov.sg/api/traffic-images/2025/10/9d879518-7d11-497e-9875-d58743b288ec.jpg",
"location": {
"latitude": 1.3605,
"longitude": 103.961412
},
"camera_id": "1112",
"image_metadata": {
"height": 1080,
"width": 1920,
"md5": "4f2232829d88823f85d6b5e3551c2839"
}
},
{
"timestamp": "2025-10-20T12:26:05+08:00",
"image": "https://images.data.gov.sg/api/traffic-images/2025/10/c7fac8a8-6c06-44e2-b20c-9f804084e27a.jpg",
"location": {
"latitude": 1.317036,
"longitude": 103.988598
},
"camera_id": "1113",
"image_metadata": {
"height": 1080,
"width": 1920,
"md5": "eb993debaeab58acd09110bd8c138c57"
}
},
{
"timestamp": "2025-10-20T12:26:05+08:00",
"image": "https://images.data.gov.sg/api/traffic-images/2025/10/865c187e-50f6-48cb-b117-98ba5dbf72ef.jpg",
"location": {
"latitude": 1.27414394350065,
"longitude": 103.851316802547
},
"camera_id": "1501",
"image_metadata": {
"height": 240,
"width": 320,
"md5": "aaef928e029ae19738104a86b3a6273e"
}
},
{
"timestamp": "2025-10-20T12:26:05+08:00",
"image": "https://images.data.gov.sg/api/traffic-images/2025/10/2b397580-2f91-465c-be1a-593fa1a4e50d.jpg",
"location": {
"latitude": 1.27135090682664,
"longitude": 103.861828440597
},
"camera_id": "1502",
"image_metadata": {
"height": 240,
"width": 320,
"md5": "7dec5de4c1263680a72708095fb6381e"
}
},
{
"timestamp": "2025-10-20T12:26:05+08:00",
"image": "https://images.data.gov.sg/api/traffic-images/2025/10/113e3529-89e6-4a15-b8b7-406094153a6b.jpg",
"location": {
"latitude": 1.27066408655104,
"longitude": 103.856977943394
},
"camera_id": "1503",
"image_metadata": {
"height": 240,
"width": 320,
"md5": "9c900b54d4d20fb8006e6b7a9b39756e"
}
},
{
"timestamp": "2025-10-20T12:26:05+08:00",
"image": "https://images.data.gov.sg/api/traffic-images/2025/10/a3302071-1a09-4f38-8612-f071257fac94.jpg",
"location": {
"latitude": 1.29409891409364,
"longitude": 103.876056196568
},
"camera_id": "1504",
"image_metadata": {
"height": 240,
"width": 320,
"md5": "37c357c9494538e0dc6bc4783b0c66ac"
}
},
{
"timestamp": "2025-10-20T12:26:05+08:00",
"image": "https://images.data.gov.sg/api/traffic-images/2025/10/fbf85625-e778-4f21-aee3-a266b1cc10e7.jpg",
"location": {
"latitude": 1.2752977149006,
"longitude": 103.866390381759
},
"camera_id": "1505",
"image_metadata": {
"height": 240,
"width": 320,
"md5": "89455dcbdb93ff03d0d57c4f6e98b093"
}
},
{
"timestamp": "2025-10-20T12:26:05+08:00",
"image": "https://images.data.gov.sg/api/traffic-images/2025/10/12de7958-80cf-4126-aa0d-c804a1a79162.jpg",
"location": {
"latitude": 1.323604823,
"longitude": 103.8587802
},
"camera_id": "1701",
"image_metadata": {
"height": 1080,
"width": 1920,
"md5": "099011b214b7731a728abef5b60bc973"
}
},
{
"timestamp": "2025-10-20T12:26:05+08:00",
"image": "https://images.data.gov.sg/api/traffic-images/2025/10/48211ac0-7db9-4a17-bfed-2a561cbb0c7b.jpg",
"location": {
"latitude": 1.34355015,
"longitude": 103.8601984
},
"camera_id": "1702",
"image_metadata": {
"height": 1080,
"width": 1920,
"md5": "78475bf99e3148ab8ed86b419e61211e"
}
},
{
"timestamp": "2025-10-20T12:26:05+08:00",
"image": "https://images.data.gov.sg/api/traffic-images/2025/10/5aedf02f-5ecd-489f-b6b1-d36c57a9e31b.jpg",
"location": {
"latitude": 1.32814722194857,
"longitude": 103.862203282048
},
"camera_id": "1703",
"image_metadata": {
"height": 1080,
"width": 1920,
"md5": "58eac614ce31f9ce4170a19a68ce3d73"
}
},
{
"timestamp": "2025-10-20T12:26:05+08:00",
"image": "https://images.data.gov.sg/api/traffic-images/2025/10/c6a17413-fa39-44f8-adef-61737c08debb.jpg",
"location": {
"latitude": 1.28569398886979,
"longitude": 103.837524510188
},
"camera_id": "1704",
"image_metadata": {
"height": 1080,
"width": 1920,
"md5": "353dd11eddec26e9fc408ca52af3240b"
}
},
{
"timestamp": "2025-10-20T12:26:05+08:00",
"image": "https://images.data.gov.sg/api/traffic-images/2025/10/517b6593-c358-4d71-b57a-1412a4ce94f5.jpg",
"location": {
"latitude": 1.375925022,
"longitude": 103.8587986
},
"camera_id": "1705",
"image_metadata": {
"height": 1080,
"width": 1920,
"md5": "aef0ad9b01dcc985b333ea5b0293c9e2"
}
},
{
"timestamp": "2025-10-20T12:26:05+08:00",
"image": "https://images.data.gov.sg/api/traffic-images/2025/10/c1f37db7-e1f7-4316-9f03-28c2bf9efb95.jpg",
"location": {
"latitude": 1.38861,
"longitude": 103.85806
},
"camera_id": "1706",
"image_metadata": {
"height": 1080,
"width": 1920,
"md5": "2df77e644a3174bc0b44e59e502cc04d"
}
},
{
"timestamp": "2025-10-20T12:26:05+08:00",
"image": "https://images.data.gov.sg/api/traffic-images/2025/10/a8e17db5-e3db-43a6-92ed-55e27318801e.jpg",
"location": {
"latitude": 1.28036584335876,
"longitude": 103.830451146503
},
"camera_id": "1707",
"image_metadata": {
"height": 1080,
"width": 1920,
"md5": "99576486111859748b8c079442a38b22"
}
},
{
"timestamp": "2025-10-20T12:26:05+08:00",
"image": "https://images.data.gov.sg/api/traffic-images/2025/10/185b4ff2-51dd-47d3-ba13-6e65d6cb70eb.jpg",
"location": {
"latitude": 1.31384231654635,
"longitude": 103.845603032574
},
"camera_id": "1709",
"image_metadata": {
"height": 1080,
"width": 1920,
"md5": "b71defcaba164d56548e0b61695d2319"
}
},
{
"timestamp": "2025-10-20T12:26:05+08:00",
"image": "https://images.data.gov.sg/api/traffic-images/2025/10/35a036dd-3084-41ac-98d2-f1bcee6515c9.jpg",
"location": {
"latitude": 1.35296,
"longitude": 103.85719
},
"camera_id": "1711",
"image_metadata": {
"height": 1080,
"width": 1920,
"md5": "c76d018ac3fb60eceba619206f3431b8"
}
},
{
"timestamp": "2025-10-20T12:26:05+08:00",
"image": "https://images.data.gov.sg/api/traffic-images/2025/10/32da0551-5f50-4654-9554-d6c0a2a787ba.jpg",
"location": {
"latitude": 1.447023728,
"longitude": 103.7716543
},
"camera_id": "2701",
"image_metadata": {
"height": 1080,
"width": 1920,
"md5": "fd0b1b4790bd51179d85d88cb23d0556"
}
},
{
"timestamp": "2025-10-20T12:26:05+08:00",
"image": "https://images.data.gov.sg/api/traffic-images/2025/10/194cb252-b356-435b-975d-3b2cad25bd73.jpg",
"location": {
"latitude": 1.445554109,
"longitude": 103.7683397
},
"camera_id": "2702",
"image_metadata": {
"height": 1080,
"width": 1920,
"md5": "c0c3354471e1c2bd41d413ca7c167dec"
}
},
{
"timestamp": "2025-10-20T12:26:05+08:00",
"image": "https://images.data.gov.sg/api/traffic-images/2025/10/1b406e8f-5e59-4777-bb88-cd624942fda1.jpg",
"location": {
"latitude": 1.35047790791386,
"longitude": 103.791033581325
},
"camera_id": "2703",
"image_metadata": {
"height": 1080,
"width": 1920,
"md5": "2c356a7b4071ed884a0aad205a2e5fee"
}
},
{
"timestamp": "2025-10-20T12:26:05+08:00",
"image": "https://images.data.gov.sg/api/traffic-images/2025/10/f2c13d7b-910e-4206-84f3-77e6cc1bf8e4.jpg",
"location": {
"latitude": 1.429588536,
"longitude": 103.769311
},
"camera_id": "2704",
"image_metadata": {
"height": 1080,
"width": 1920,
"md5": "8258a6d912072e78144569297ae3d2d8"
}
},
{
"timestamp": "2025-10-20T12:26:05+08:00",
"image": "https://images.data.gov.sg/api/traffic-images/2025/10/55f28d0b-cb29-46a0-977b-770acfc320d6.jpg",
"location": {
"latitude": 1.36728572,
"longitude": 103.7794698
},
"camera_id": "2705",
"image_metadata": {
"height": 1080,
"width": 1920,
"md5": "0bfc289723693f30aa36fb1342bf0c82"
}
},
{
"timestamp": "2025-10-20T12:26:05+08:00",
"image": "https://images.data.gov.sg/api/traffic-images/2025/10/05bb53d0-b515-4d75-a950-1849aed6384a.jpg",
"location": {
"latitude": 1.414142,
"longitude": 103.771168
},
"camera_id": "2706",
"image_metadata": {
"height": 1080,
"width": 1920,
"md5": "a2c61f5ae4990394e825cf6f0997d7db"
}
},
{
"timestamp": "2025-10-20T12:26:05+08:00",
"image": "https://images.data.gov.sg/api/traffic-images/2025/10/60e06557-578c-42cb-b326-fb57c18b668c.jpg",
"location": {
"latitude": 1.3983,
"longitude": 103.774247
},
"camera_id": "2707",
"image_metadata": {
"height": 1080,
"width": 1920,
"md5": "93541a677d868d209c44a19e0f9abd72"
}
},
{
"timestamp": "2025-10-20T12:26:05+08:00",
"image": "https://images.data.gov.sg/api/traffic-images/2025/10/3ae6539c-0568-4be1-89f2-4dafd3cc12a5.jpg",
"location": {
"latitude": 1.3865,
"longitude": 103.7747
},
"camera_id": "2708",
"image_metadata": {
"height": 360,
"width": 640,
"md5": "675e9ac175517dd2fcc9b302f25fe825"
}
},
{
"timestamp": "2025-10-20T12:26:05+08:00",
"image": "https://images.data.gov.sg/api/traffic-images/2025/10/0d8ac0a2-edcd-4ab8-8b5c-fb53536357ad.jpg",
"location": {
"latitude": 1.33831,
"longitude": 103.98032
},
"camera_id": "3702",
"image_metadata": {
"height": 1080,
"width": 1920,
"md5": "b22ff8dbd39356e45cc0b80566659648"
}
},
{
"timestamp": "2025-10-20T12:26:05+08:00",
"image": "https://images.data.gov.sg/api/traffic-images/2025/10/42ac7568-3c98-4462-b191-bf520c193013.jpg",
"location": {
"latitude": 1.2958550156561,
"longitude": 103.880314665981
},
"camera_id": "3704",
"image_metadata": {
"height": 1080,
"width": 1920,
"md5": "de3422b415174eeb65dcfdf67e506a12"
}
},
{
"timestamp": "2025-10-20T12:26:05+08:00",
"image": "https://images.data.gov.sg/api/traffic-images/2025/10/1d6905f6-6449-40ad-bbf9-b4822c125416.jpg",
"location": {
"latitude": 1.32743,
"longitude": 103.97383
},
"camera_id": "3705",
"image_metadata": {
"height": 1080,
"width": 1920,
"md5": "c713fff2c59b637a9b69487703b55e0f"
}
},
{
"timestamp": "2025-10-20T12:26:05+08:00",
"image": "https://images.data.gov.sg/api/traffic-images/2025/10/23e0ff67-e59e-4c14-b97d-3a761d2256e6.jpg",
"location": {
"latitude": 1.309330837,
"longitude": 103.9350504
},
"camera_id": "3793",
"image_metadata": {
"height": 1080,
"width": 1920,
"md5": "afa877a1077e1d9ed143de5805b98cc6"
}
},
{
"timestamp": "2025-10-20T12:26:05+08:00",
"image": "https://images.data.gov.sg/api/traffic-images/2025/10/f51ef16b-e900-4905-b358-21b88ecd2133.jpg",
"location": {
"latitude": 1.30145145166066,
"longitude": 103.910596320237
},
"camera_id": "3795",
"image_metadata": {
"height": 1080,
"width": 1920,
"md5": "7083c3a757bbbd98b4891000fba33e76"
}
},
{
"timestamp": "2025-10-20T12:26:05+08:00",
"image": "https://images.data.gov.sg/api/traffic-images/2025/10/150d6c63-fe1e-438a-bad4-2f74fca92264.jpg",
"location": {
"latitude": 1.297512569,
"longitude": 103.8983019
},
"camera_id": "3796",
"image_metadata": {
"height": 1080,
"width": 1920,
"md5": "328f966d437d75bf1ae569c911d8e499"
}
},
{
"timestamp": "2025-10-20T12:26:05+08:00",
"image": "https://images.data.gov.sg/api/traffic-images/2025/10/c2283b42-e751-41bb-9bc8-1e074f2751d8.jpg",
"location": {
"latitude": 1.29565733262976,
"longitude": 103.885283049309
},
"camera_id": "3797",
"image_metadata": {
"height": 1080,
"width": 1920,
"md5": "0f1f62b2d8bfafdfbc5f4071a4f2e3c5"
}
},
{
"timestamp": "2025-10-20T12:26:05+08:00",
"image": "https://images.data.gov.sg/api/traffic-images/2025/10/1f6f651e-1753-4ea5-bc84-28f360577940.jpg",
"location": {
"latitude": 1.29158484,
"longitude": 103.8615987
},
"camera_id": "3798",
"image_metadata": {
"height": 1080,
"width": 1920,
"md5": "72cd201e9f99ebbaf20fe6b6aa741fc8"
}
},
{
"timestamp": "2025-10-20T12:26:05+08:00",
"image": "https://images.data.gov.sg/api/traffic-images/2025/10/804d8776-4bc0-493f-a15d-95ecb7d42c94.jpg",
"location": {
"latitude": 1.2871,
"longitude": 103.79633
},
"camera_id": "4701",
"image_metadata": {
"height": 1080,
"width": 1920,
"md5": "17e94f3a0b994bb2e102d706eb49a674"
}
},
{
"timestamp": "2025-10-20T12:26:05+08:00",
"image": "https://images.data.gov.sg/api/traffic-images/2025/10/517a75a8-fba1-4be2-9ec5-c7c58f2fd918.jpg",
"location": {
"latitude": 1.27237,
"longitude": 103.8324
},
"camera_id": "4702",
"image_metadata": {
"height": 1080,
"width": 1920,
"md5": "526eb4d4a990d94625edb48ec22f1e08"
}
},
{
"timestamp": "2025-10-20T12:26:05+08:00",
"image": "https://images.data.gov.sg/api/traffic-images/2025/10/14c5be69-11dc-4e25-bd37-4842ac1a9cc7.jpg",
"location": {
"latitude": 1.348697862,
"longitude": 103.6350413
},
"camera_id": "4703",
"image_metadata": {
"height": 1080,
"width": 1920,
"md5": "ec11921c8f629a273b3ff7b19bfe1121"
}
},
{
"timestamp": "2025-10-20T12:26:05+08:00",
"image": "https://images.data.gov.sg/api/traffic-images/2025/10/8836a45c-0f1e-4d5a-bbbe-c66d01e4cf29.jpg",
"location": {
"latitude": 1.27877,
"longitude": 103.82375
},
"camera_id": "4704",
"image_metadata": {
"height": 1080,
"width": 1920,
"md5": "946aba346ae639426242431cb0724e0d"
}
},
{
"timestamp": "2025-10-20T12:26:05+08:00",
"image": "https://images.data.gov.sg/api/traffic-images/2025/10/a722efe4-04f1-46d4-9175-4249963d5e33.jpg",
"location": {
"latitude": 1.32618,
"longitude": 103.73028
},
"camera_id": "4705",
"image_metadata": {
"height": 1080,
"width": 1920,
"md5": "19a1bbd38e83440b622eb6b7c224c71a"
}
},
{
"timestamp": "2025-10-20T12:26:05+08:00",
"image": "https://images.data.gov.sg/api/traffic-images/2025/10/2da9c87b-6ff2-4914-bbae-1491e3a5539b.jpg",
"location": {
"latitude": 1.29792,
"longitude": 103.78205
},
"camera_id": "4706",
"image_metadata": {
"height": 1080,
"width": 1920,
"md5": "42235c1bde4b732e57d9a22ba973ae65"
}
},
{
"timestamp": "2025-10-20T12:26:05+08:00",
"image": "https://images.data.gov.sg/api/traffic-images/2025/10/1ce0e295-0077-46a8-97c9-14edfe3806bf.jpg",
"location": {
"latitude": 1.33344648135658,
"longitude": 103.652700847056
},
"camera_id": "4707",
"image_metadata": {
"height": 1080,
"width": 1920,
"md5": "746d9873aca2c5fbe5c8168db1a1198a"
}
},
{
"timestamp": "2025-10-20T12:26:05+08:00",
"image": "https://images.data.gov.sg/api/traffic-images/2025/10/195dd162-e465-4267-9a0a-23f5055c3f41.jpg",
"location": {
"latitude": 1.29939,
"longitude": 103.7799
},
"camera_id": "4708",
"image_metadata": {
"height": 1080,
"width": 1920,
"md5": "7039e135b5c153f52721ae985b5cac93"
}
},
{
"timestamp": "2025-10-20T12:26:05+08:00",
"image": "https://images.data.gov.sg/api/traffic-images/2025/10/6e892a7e-319b-4204-a2c5-edefb5c92467.jpg",
"location": {
"latitude": 1.312019,
"longitude": 103.763002
},
"camera_id": "4709",
"image_metadata": {
"height": 1080,
"width": 1920,
"md5": "9745645e35b11644beeae5fdfb483593"
}
},
{
"timestamp": "2025-10-20T12:26:05+08:00",
"image": "https://images.data.gov.sg/api/traffic-images/2025/10/1bfaabd1-6ee8-4295-8709-7bfd888fa535.jpg",
"location": {
"latitude": 1.32153,
"longitude": 103.75273
},
"camera_id": "4710",
"image_metadata": {
"height": 1080,
"width": 1920,
"md5": "d3bbed8c0203c08aae3a04436f0ca9a5"
}
},
{
"timestamp": "2025-10-20T12:26:05+08:00",
"image": "https://images.data.gov.sg/api/traffic-images/2025/10/8dfa9e6e-1e71-4173-a890-87a196157259.jpg",
"location": {
"latitude": 1.341244001,
"longitude": 103.6439134
},
"camera_id": "4712",
"image_metadata": {
"height": 1080,
"width": 1920,
"md5": "94b25927a384d5b0617e61e0ef3dd27d"
}
},
{
"timestamp": "2025-10-20T12:26:05+08:00",
"image": "https://images.data.gov.sg/api/traffic-images/2025/10/b0b1d80a-0151-42ae-ac6a-93166d4dd867.jpg",
"location": {
"latitude": 1.347645829,
"longitude": 103.6366955
},
"camera_id": "4713",
"image_metadata": {
"height": 1080,
"width": 1920,
"md5": "e50082bbc1ef510e02c75db70c18a62f"
}
},
{
"timestamp": "2025-10-20T12:26:05+08:00",
"image": "https://images.data.gov.sg/api/traffic-images/2025/10/108a0883-0eea-46ff-93ba-a31668abdc85.jpg",
"location": {
"latitude": 1.31023,
"longitude": 103.76438
},
"camera_id": "4714",
"image_metadata": {
"height": 1080,
"width": 1920,
"md5": "82c7d501086a307862e6f15e91ecd659"
}
},
{
"timestamp": "2025-10-20T12:26:05+08:00",
"image": "https://images.data.gov.sg/api/traffic-images/2025/10/f2a8d0d6-8246-49c1-b444-2841308b5d68.jpg",
"location": {
"latitude": 1.32227,
"longitude": 103.67453
},
"camera_id": "4716",
"image_metadata": {
"height": 1080,
"width": 1920,
"md5": "480a24e7347a3b3a371e56c96b32b3e5"
}
},
{
"timestamp": "2025-10-20T12:26:05+08:00",
"image": "https://images.data.gov.sg/api/traffic-images/2025/10/78f31cdd-0be0-407b-a5c1-4c238f734ef4.jpg",
"location": {
"latitude": 1.25999999687243,
"longitude": 103.823611110166
},
"camera_id": "4798",
"image_metadata": {
"height": 1080,
"width": 1920,
"md5": "baf0ff0dec9ebd583f9dd7e06a8f2a8d"
}
},
{
"timestamp": "2025-10-20T12:26:05+08:00",
"image": "https://images.data.gov.sg/api/traffic-images/2025/10/2a5a67cc-b796-413a-898a-c95235b6775e.jpg",
"location": {
"latitude": 1.26027777363278,
"longitude": 103.823888890049
},
"camera_id": "4799",
"image_metadata": {
"height": 1080,
"width": 1920,
"md5": "897525a66677a90fa2ea6df62ab598e7"
}
},
{
"timestamp": "2025-10-20T12:26:05+08:00",
"image": "https://images.data.gov.sg/api/traffic-images/2025/10/7054d519-69a4-4968-839e-7509f467fedb.jpg",
"location": {
"latitude": 1.3309693,
"longitude": 103.9168616
},
"camera_id": "5794",
"image_metadata": {
"height": 1080,
"width": 1920,
"md5": "8eddd7e5264557f4619c4cfa189eb99c"
}
},
{
"timestamp": "2025-10-20T12:26:05+08:00",
"image": "https://images.data.gov.sg/api/traffic-images/2025/10/57cd5e48-6060-42a0-bfec-1146bec99218.jpg",
"location": {
"latitude": 1.326024822,
"longitude": 103.905625
},
"camera_id": "5795",
"image_metadata": {
"height": 1080,
"width": 1920,
"md5": "8f8ff1dc88c839f47389668b6143918f"
}
},
{
"timestamp": "2025-10-20T12:26:05+08:00",
"image": "https://images.data.gov.sg/api/traffic-images/2025/10/771e2aed-5525-4a41-91a3-0383e183f3bd.jpg",
"location": {
"latitude": 1.322875288,
"longitude": 103.8910793
},
"camera_id": "5797",
"image_metadata": {
"height": 1080,
"width": 1920,
"md5": "8c8c9a80b29836f2da6b38cad044e503"
}
},
{
"timestamp": "2025-10-20T12:26:05+08:00",
"image": "https://images.data.gov.sg/api/traffic-images/2025/10/95a6008a-96ff-49d0-80e5-9de2bc3c85ee.jpg",
"location": {
"latitude": 1.32036078126842,
"longitude": 103.877174116489
},
"camera_id": "5798",
"image_metadata": {
"height": 1080,
"width": 1920,
"md5": "d52017cc9ecf05e7b7f9fa996126453c"
}
},
{
"timestamp": "2025-10-20T12:26:05+08:00",
"image": "https://images.data.gov.sg/api/traffic-images/2025/10/b2556e63-52b1-424d-93bc-583ae97ef785.jpg",
"location": {
"latitude": 1.328171608,
"longitude": 103.8685191
},
"camera_id": "5799",
"image_metadata": {
"height": 1080,
"width": 1920,
"md5": "c502eb511c25c3821508af5df635465c"
}
},
{
"timestamp": "2025-10-20T12:26:05+08:00",
"image": "https://images.data.gov.sg/api/traffic-images/2025/10/72089388-5aad-48db-8243-c0523df50071.jpg",
"location": {
"latitude": 1.329334,
"longitude": 103.858222
},
"camera_id": "6701",
"image_metadata": {
"height": 1080,
"width": 1920,
"md5": "43f3e56ba19d721ca7e800634651f583"
}
},
{
"timestamp": "2025-10-20T12:26:05+08:00",
"image": "https://images.data.gov.sg/api/traffic-images/2025/10/6d04b74a-9b50-4b63-97d7-d9bae8c02bb5.jpg",
"location": {
"latitude": 1.328899,
"longitude": 103.84121
},
"camera_id": "6703",
"image_metadata": {
"height": 1080,
"width": 1920,
"md5": "57184f2ee8cc3fe3984b44d860b5b778"
}
},
{
"timestamp": "2025-10-20T12:26:05+08:00",
"image": "https://images.data.gov.sg/api/traffic-images/2025/10/a8f778a4-4167-48dc-adac-fc6c8f361e28.jpg",
"location": {
"latitude": 1.32657403632366,
"longitude": 103.826857295633
},
"camera_id": "6704",
"image_metadata": {
"height": 1080,
"width": 1920,
"md5": "917b01b2327016199500dc5e86f41d8a"
}
},
{
"timestamp": "2025-10-20T12:26:05+08:00",
"image": "https://images.data.gov.sg/api/traffic-images/2025/10/3f095086-b438-4b49-bdaa-35805d5dd87f.jpg",
"location": {
"latitude": 1.332124,
"longitude": 103.81768
},
"camera_id": "6705",
"image_metadata": {
"height": 1080,
"width": 1920,
"md5": "1ef5a507edbeb9d66f44350bd83b5473"
}
},
{
"timestamp": "2025-10-20T12:26:05+08:00",
"image": "https://images.data.gov.sg/api/traffic-images/2025/10/e4cfd21a-8c49-4e20-abca-3755642bc225.jpg",
"location": {
"latitude": 1.349428893,
"longitude": 103.7952799
},
"camera_id": "6706",
"image_metadata": {
"height": 1080,
"width": 1920,
"md5": "534a9364e4a7bef033dcdfb94fc1ce5b"
}
},
{
"timestamp": "2025-10-20T12:26:05+08:00",
"image": "https://images.data.gov.sg/api/traffic-images/2025/10/d0f70fc6-3507-4cc0-8c3a-462589c9d541.jpg",
"location": {
"latitude": 1.345996,
"longitude": 103.69016
},
"camera_id": "6708",
"image_metadata": {
"height": 1080,
"width": 1920,
"md5": "ad1417171a919b18c23f9b9306718e59"
}
},
{
"timestamp": "2025-10-20T12:26:05+08:00",
"image": "https://images.data.gov.sg/api/traffic-images/2025/10/19318eed-9928-4945-b8c2-63d4ab7c1b4a.jpg",
"location": {
"latitude": 1.344205,
"longitude": 103.78577
},
"camera_id": "6710",
"image_metadata": {
"height": 1080,
"width": 1920,
"md5": "134648ef6d35cbe85dc8bdee5d21bd4a"
}
},
{
"timestamp": "2025-10-20T12:26:05+08:00",
"image": "https://images.data.gov.sg/api/traffic-images/2025/10/e2718173-10bc-43c8-96a8-0b962279cfe2.jpg",
"location": {
"latitude": 1.33771,
"longitude": 103.977827
},
"camera_id": "6711",
"image_metadata": {
"height": 1080,
"width": 1920,
"md5": "14805b746c6bb1e6642486604b2e1d18"
}
},
{
"timestamp": "2025-10-20T12:26:05+08:00",
"image": "https://images.data.gov.sg/api/traffic-images/2025/10/5a162bdd-89fe-45e4-a335-02648d61b070.jpg",
"location": {
"latitude": 1.332691,
"longitude": 103.770278
},
"camera_id": "6712",
"image_metadata": {
"height": 1080,
"width": 1920,
"md5": "c96ae8fcbf2132caee85ffe42a94866d"
}
},
{
"timestamp": "2025-10-20T12:26:05+08:00",
"image": "https://images.data.gov.sg/api/traffic-images/2025/10/6c3fdcb8-2c30-412e-91a1-9ab363fb6b25.jpg",
"location": {
"latitude": 1.340298,
"longitude": 103.945652
},
"camera_id": "6713",
"image_metadata": {
"height": 1080,
"width": 1920,
"md5": "8fc3a14f83904063a5c6b478fa20af17"
}
},
{
"timestamp": "2025-10-20T12:26:05+08:00",
"image": "https://images.data.gov.sg/api/traffic-images/2025/10/368a6bea-18d8-412f-8408-b3b8b790403a.jpg",
"location": {
"latitude": 1.361742,
"longitude": 103.703341
},
"camera_id": "6714",
"image_metadata": {
"height": 1080,
"width": 1920,
"md5": "0127cf668ac4743411d3a4861d3c26dc"
}
},
{
"timestamp": "2025-10-20T12:26:05+08:00",
"image": "https://images.data.gov.sg/api/traffic-images/2025/10/62ad43b5-c486-4e5d-8781-b9207f085edb.jpg",
"location": {
"latitude": 1.356299,
"longitude": 103.716071
},
"camera_id": "6715",
"image_metadata": {
"height": 1080,
"width": 1920,
"md5": "f2fd85fdeacf6434c73952bc74dd22d1"
}
},
{
"timestamp": "2025-10-20T12:26:05+08:00",
"image": "https://images.data.gov.sg/api/traffic-images/2025/10/ae62fbf3-80fb-45b6-bdb9-3880c648077e.jpg",
"location": {
"latitude": 1.322893,
"longitude": 103.6635051
},
"camera_id": "6716",
"image_metadata": {
"height": 1080,
"width": 1920,
"md5": "57c67c6fd253b35d47d776cceea44016"
}
},
{
"timestamp": "2025-10-20T12:26:05+08:00",
"image": "https://images.data.gov.sg/api/traffic-images/2025/10/b11fb989-bd1d-4a55-9f15-caa94008d1a3.jpg",
"location": {
"latitude": 1.354245,
"longitude": 103.963782
},
"camera_id": "7791",
"image_metadata": {
"height": 1080,
"width": 1920,
"md5": "eaf286cbfbbe325bfd8f022c16a9feb8"
}
},
{
"timestamp": "2025-10-20T12:26:05+08:00",
"image": "https://images.data.gov.sg/api/traffic-images/2025/10/98952091-9154-49c3-8699-d792a643037d.jpg",
"location": {
"latitude": 1.37704704,
"longitude": 103.92946983
},
"camera_id": "7793",
"image_metadata": {
"height": 1080,
"width": 1920,
"md5": "747026392565bfc7ac9c1c3d25b7cb73"
}
},
{
"timestamp": "2025-10-20T12:26:05+08:00",
"image": "https://images.data.gov.sg/api/traffic-images/2025/10/4b28a21e-6b57-4db0-9d8c-e6fc411195f5.jpg",
"location": {
"latitude": 1.37988658,
"longitude": 103.92009174
},
"camera_id": "7794",
"image_metadata": {
"height": 1080,
"width": 1920,
"md5": "791141c874244c1073aacd5fdcfe9ebe"
}
},
{
"timestamp": "2025-10-20T12:26:05+08:00",
"image": "https://images.data.gov.sg/api/traffic-images/2025/10/bafd5b33-ddcd-4c8a-85a0-fe8379373ba8.jpg",
"location": {
"latitude": 1.38432741,
"longitude": 103.91585701
},
"camera_id": "7795",
"image_metadata": {
"height": 1080,
"width": 1920,
"md5": "2cb01611ac1485b9d6d435951e49e3a5"
}
},
{
"timestamp": "2025-10-20T12:26:05+08:00",
"image": "https://images.data.gov.sg/api/traffic-images/2025/10/067c88db-783d-4edd-a918-c5063832d4e6.jpg",
"location": {
"latitude": 1.39559294,
"longitude": 103.90515712
},
"camera_id": "7796",
"image_metadata": {
"height": 1080,
"width": 1920,
"md5": "d729212fa54e781694f9a4b2181d0a66"
}
},
{
"timestamp": "2025-10-20T12:26:05+08:00",
"image": "https://images.data.gov.sg/api/traffic-images/2025/10/506776bb-9a72-40fd-a67c-b9cd1be984b7.jpg",
"location": {
"latitude": 1.40002575,
"longitude": 103.85702534
},
"camera_id": "7797",
"image_metadata": {
"height": 1080,
"width": 1920,
"md5": "0a21311ec36276fdcd3998edb0d89688"
}
},
{
"timestamp": "2025-10-20T12:26:05+08:00",
"image": "https://images.data.gov.sg/api/traffic-images/2025/10/b644074e-f4a2-47a6-8b7f-9e90d60a06f9.jpg",
"location": {
"latitude": 1.39748842,
"longitude": 103.85400467
},
"camera_id": "7798",
"image_metadata": {
"height": 1080,
"width": 1920,
"md5": "ac7da170fb280374d378ea48ed474f45"
}
},
{
"timestamp": "2025-10-20T12:26:05+08:00",
"image": "https://images.data.gov.sg/api/traffic-images/2025/10/6a2318bd-e700-4ba4-b770-a784fcd85b8b.jpg",
"location": {
"latitude": 1.38647,
"longitude": 103.74143
},
"camera_id": "8701",
"image_metadata": {
"height": 1080,
"width": 1920,
"md5": "71dd350c1975fa5826e53c8e9a545a3b"
}
},
{
"timestamp": "2025-10-20T12:26:05+08:00",
"image": "https://images.data.gov.sg/api/traffic-images/2025/10/32542bc1-2e15-4b44-828b-ac1ec1bb9960.jpg",
"location": {
"latitude": 1.39059,
"longitude": 103.7717
},
"camera_id": "8702",
"image_metadata": {
"height": 1080,
"width": 1920,
"md5": "742757026edde5f27a2a7db09ec9b90e"
}
},
{
"timestamp": "2025-10-20T12:26:05+08:00",
"image": "https://images.data.gov.sg/api/traffic-images/2025/10/155ed763-39de-49f9-9c72-ffc85c2c0391.jpg",
"location": {
"latitude": 1.3899,
"longitude": 103.74843
},
"camera_id": "8704",
"image_metadata": {
"height": 1080,
"width": 1920,
"md5": "8a1f17a812b0ee158eb4b60f9c70a696"
}
},
{
"timestamp": "2025-10-20T12:26:05+08:00",
"image": "https://images.data.gov.sg/api/traffic-images/2025/10/8e71f3d9-9788-4b14-82db-cd9f28f43bc8.jpg",
"location": {
"latitude": 1.3664,
"longitude": 103.70899
},
"camera_id": "8706",
"image_metadata": {
"height": 1080,
"width": 1920,
"md5": "bf6efb812a9282a33c593ddbbd00a5ee"
}
},
{
"timestamp": "2025-10-20T12:26:05+08:00",
"image": "https://images.data.gov.sg/api/traffic-images/2025/10/6684013f-67e8-4db4-9f06-4435a3bc347b.jpg",
"location": {
"latitude": 1.39466333,
"longitude": 103.83474601
},
"camera_id": "9701",
"image_metadata": {
"height": 1080,
"width": 1920,
"md5": "d62995dda70ab03498bfc0dc74bba2ab"
}
},
{
"timestamp": "2025-10-20T12:26:05+08:00",
"image": "https://images.data.gov.sg/api/traffic-images/2025/10/2124448a-756f-40df-96d6-258ca98036d1.jpg",
"location": {
"latitude": 1.39474081,
"longitude": 103.81797086
},
"camera_id": "9702",
"image_metadata": {
"height": 1080,
"width": 1920,
"md5": "e428167992c0694f0719e26b70b7c069"
}
},
{
"timestamp": "2025-10-20T12:26:05+08:00",
"image": "https://images.data.gov.sg/api/traffic-images/2025/10/f651add2-4b3d-4eae-b031-0ce35408238d.jpg",
"location": {
"latitude": 1.422857,
"longitude": 103.773005
},
"camera_id": "9703",
"image_metadata": {
"height": 1080,
"width": 1920,
"md5": "52d9df67c90414a5179bde1e4a70e1f8"
}
},
{
"timestamp": "2025-10-20T12:26:05+08:00",
"image": "https://images.data.gov.sg/api/traffic-images/2025/10/0ecc99a3-014d-42b0-b8e3-224ecd108ac5.jpg",
"location": {
"latitude": 1.42214311,
"longitude": 103.79542062
},
"camera_id": "9704",
"image_metadata": {
"height": 1080,
"width": 1920,
"md5": "48bacb7d335405bf3b5a0cf62b0024a5"
}
},
{
"timestamp": "2025-10-20T12:26:05+08:00",
"image": "https://images.data.gov.sg/api/traffic-images/2025/10/466c0aea-8a01-44a3-bcf8-5c67258c3b1e.jpg",
"location": {
"latitude": 1.42627712,
"longitude": 103.78716637
},
"camera_id": "9705",
"image_metadata": {
"height": 1080,
"width": 1920,
"md5": "e56340e44278a3f70a793550323d6feb"
}
},
{
"timestamp": "2025-10-20T12:26:05+08:00",
"image": "https://images.data.gov.sg/api/traffic-images/2025/10/d35347b0-a24b-42de-8628-60a4a4bea07c.jpg",
"location": {
"latitude": 1.41270056,
"longitude": 103.80642712
},
"camera_id": "9706",
"image_metadata": {
"height": 1080,
"width": 1920,
"md5": "1ab5a98b4854a18f64a6d9eac6e5b91a"
}
}
]
}
],
"api_info": {
"status": "healthy"
}
}
