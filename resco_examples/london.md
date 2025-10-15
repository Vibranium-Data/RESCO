## Example: London Traffic - Road Disruptions

Domain: Mobility

Data source: [Transport for London (TFL) Data](https://tfl.gov.uk/info-for/open-data-users/our-open-data)
Register for the TFL API to gain access [here](https://api-portal.tfl.gov.uk/).

### 1. London Road Traffic Disruptions as Events

**Roads as Entities**

{
"$type": "Tfl.Api.Presentation.Entities.RoadDisruption, Tfl.Api.Presentation.Entities",
    "id": "TIMS-217284",
    "url": "/Road/All/Disruption/TIMS-217284",
    "point": "[-0.2531,51.486126]",
    "severity": "Moderate",
    "ordinal": 5,
    "category": "Works",
    "subCategory": "Utility works",
    "comments": "[A316] Burlington Lane (Northbound) at the junction of [A4] Hogarth Lane - There is no northbound access onto Hogarth Roundabout from Burlington Lane due to emergency gas main repairs. Hogarth Flyover remains open.",
    "currentUpdate": "Delays are possible. ",
    "currentUpdateDateTime": "2025-10-15T14:52:00Z",
    "corridorIds": ["a316", "a4"],
    "startDateTime": "2025-09-28T19:00:00Z",
    "endDateTime": "2025-10-24T19:00:00Z",
    "lastModifiedTime": "2025-10-15T16:27:35Z",
    "levelOfInterest": "High",
    "location": "[A316] BURLINGTON LANE (W4 ) (Hounslow)",
    "status": "Active",
    "geography": {
        "type": "Point",
        "coordinates": [-0.2531, 51.486126],
        "crs": {
            "type": "name",
            "properties": {
                "name": "EPSG:4326"
            }
        }
    },
    "geometry": {
        "type": "Polygon",
        "coordinates": [
            [
                [-0.2545495351, 51.4856983394],
                [-0.2544455493, 51.4854565686],
                [-0.2541951599, 51.4853021558],
                [-0.2538066624, 51.4852402162],
                [-0.2534253613, 51.4853176493],
                [-0.2525333654, 51.4857686828],
                [-0.2520446386, 51.4861133861],
                [-0.2518418455, 51.4863719034],
                [-0.2517579897, 51.4865980996],
                [-0.2517749791, 51.4867513953],
                [-0.2518939102, 51.4869102481],
                [-0.2521011617, 51.487028594],
                [-0.2523651808, 51.4870884151],
                [-0.2526457713, 51.4870806037],
                [-0.252900214, 51.4870063493],
                [-0.2530897706, 51.4868769568],
                [-0.2532041313, 51.4866691774],
                [-0.2533503868, 51.4865316361],
                [-0.2543883929, 51.4859728778],
                [-0.2545057266, 51.4858440193],
                [-0.2545495351, 51.4856983394]
            ]
        ],
        "crs": {
            "type": "name",
            "properties": {
                "name": "EPSG:4326"
            }
        }
    },
    "streets": [{
        "$type": "Tfl.Api.Presentation.Entities.Street, Tfl.Api.Presentation.Entities",
"name": "[A316] BURLINGTON LANE (W4 )",
"closure": "Closed",
"directions": "Northbound",
"segments": [{
"$type": "Tfl.Api.Presentation.Entities.StreetSegment, Tfl.Api.Presentation.Entities",
            "toid": "0",
            "lineString": "[[-0.25383,51.485689],[-0.252474,51.486644]]",
            "sourceSystemId": 0
        }, {
            "$type": "Tfl.Api.Presentation.Entities.StreetSegment, Tfl.Api.Presentation.Entities",
"toid": "0",
"lineString": "[[-0.254126,51.485558],[-0.25383,51.485689]]",
"sourceSystemId": 0
}],
"sourceSystemId": 217284,
"sourceSystemKey": "TIMS"
}],
"isProvisional": false,
"hasClosures": false,
"roadDisruptionLines": [],
"roadDisruptionImpactAreas": [],
"recurringSchedules": []
}, {
"$type": "Tfl.Api.Presentation.Entities.RoadDisruption, Tfl.Api.Presentation.Entities",
    "id": "TIMS-200007",
    "url": "/Road/All/Disruption/TIMS-200007",
    "point": "[-0.087718,51.512021]",
    "severity": "Moderate",
    "ordinal": 6,
    "category": "Works",
    "subCategory": "Borough works",
    "comments": "King William Street (Southbound) at the junction of Lombard Street - Road closed to facilitate urban realm works.",
    "currentUpdate": "Use an alternative route. Delays are possible on diversion. ",
    "currentUpdateDateTime": "2025-10-15T12:49:02Z",
    "corridorIds": ["bishopsgate cross route"],
    "startDateTime": "2024-07-08T07:00:00Z",
    "endDateTime": "2026-04-30T19:00:00Z",
    "lastModifiedTime": "2025-10-15T12:49:06Z",
    "levelOfInterest": "High",
    "location": "KING WILLIAM STREET (EC3V,EC4N,EC4R) (City of London)",
    "status": "Active",
    "geography": {
        "type": "Point",
        "coordinates": [-0.087718, 51.512021],
        "crs": {
            "type": "name",
            "properties": {
                "name": "EPSG:4326"
            }
        }
    },
    "geometry": {
        "type": "Polygon",
        "coordinates": [
            [
                [-0.0891778645, 51.5128805527],
                [-0.0890172242, 51.5125200354],
                [-0.0874801776, 51.5106900431],
                [-0.0872453036, 51.5105730268],
                [-0.0867677274, 51.51046977],
                [-0.0864870754, 51.510478646],
                [-0.0862053951, 51.5105674595],
                [-0.0860636998, 51.5106653138],
                [-0.0859642518, 51.5108058878],
                [-0.0859465127, 51.5109591496],
                [-0.0859981821, 51.5110870298],
                [-0.0861546639, 51.5112326769],
                [-0.08639087, 51.5113304629],
                [-0.0878833614, 51.5131507153],
                [-0.0880131221, 51.5132330795],
                [-0.0882300323, 51.5133058445],
                [-0.0884735516, 51.5133287601],
                [-0.0886565494, 51.5133113892],
                [-0.0888264081, 51.5132654908],
                [-0.0890132755, 51.5131654043],
                [-0.0891351782, 51.5130318883],
                [-0.0891778645, 51.5128805527]
            ]
        ],
        "crs": {
            "type": "name",
            "properties": {
                "name": "EPSG:4326"
            }
        }
    },
    "streets": [{
        "$type": "Tfl.Api.Presentation.Entities.Street, Tfl.Api.Presentation.Entities",
"name": "KING WILLIAM STREET (EC3V,EC4N,EC4R)",
"closure": "Closed",
"directions": "Southbound",
"segments": [{
"$type": "Tfl.Api.Presentation.Entities.StreetSegment, Tfl.Api.Presentation.Entities",
            "toid": "0",
            "lineString": "[[-0.088143,51.51247],[-0.088264,51.512631]]",
            "sourceSystemId": 0
        }, {
            "$type": "Tfl.Api.Presentation.Entities.StreetSegment, Tfl.Api.Presentation.Entities",
"toid": "0",
"lineString": "[[-0.087512,51.511713],[-0.087758,51.512023]]",
"sourceSystemId": 0
}, {
"$type": "Tfl.Api.Presentation.Entities.StreetSegment, Tfl.Api.Presentation.Entities",
            "toid": "0",
            "lineString": "[[-0.088403,51.512798],[-0.088458,51.512879]]",
            "sourceSystemId": 0
        }, {
            "$type": "Tfl.Api.Presentation.Entities.StreetSegment, Tfl.Api.Presentation.Entities",
"toid": "0",
"lineString": "[[-0.087758,51.512023],[-0.087868,51.51215]]",
"sourceSystemId": 0
}, {
"$type": "Tfl.Api.Presentation.Entities.StreetSegment, Tfl.Api.Presentation.Entities",
            "toid": "0",
            "lineString": "[[-0.088264,51.512631],[-0.088403,51.512798]]",
            "sourceSystemId": 0
        }, {
            "$type": "Tfl.Api.Presentation.Entities.StreetSegment, Tfl.Api.Presentation.Entities",
"toid": "0",
"lineString": "[[-0.087375,51.511549],[-0.087512,51.511713]]",
"sourceSystemId": 0
}, {
"$type": "Tfl.Api.Presentation.Entities.StreetSegment, Tfl.Api.Presentation.Entities",
            "toid": "0",
            "lineString": "[[-0.086923,51.510975],[-0.087155,51.511294]]",
            "sourceSystemId": 0
        }, {
            "$type": "Tfl.Api.Presentation.Entities.StreetSegment, Tfl.Api.Presentation.Entities",
"toid": "0",
"lineString": "[[-0.086923,51.510975],[-0.086663,51.510914]]",
"sourceSystemId": 0
}, {
"$type": "Tfl.Api.Presentation.Entities.StreetSegment, Tfl.Api.Presentation.Entities",
            "toid": "0",
            "lineString": "[[-0.087155,51.511294],[-0.087375,51.511549]]",
            "sourceSystemId": 0
        }, {
            "$type": "Tfl.Api.Presentation.Entities.StreetSegment, Tfl.Api.Presentation.Entities",
"toid": "0",
"lineString": "[[-0.087868,51.51215],[-0.088143,51.51247]]",
"sourceSystemId": 0
}],
"sourceSystemId": 200007,
"sourceSystemKey": "TIMS"
}],
"isProvisional": false,
"hasClosures": false,
"roadDisruptionLines": [],
"roadDisruptionImpactAreas": [],
"recurringSchedules": []
},
