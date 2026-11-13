---
---

# MDS Data Offers Vocabulary — 2026/1

> **Status — DRAFT.** This document specifies the data offers vocabulary of profile version `2026/1` of the [Mobility Data Space dataspace profile](https://mobility-data-space.github.io/mds-profile/2026/1/). It is not yet released.

## Introduction

This document specifies the MDS data offers vocabulary: which properties an MDS asset has, which of them are required, and which values some of them take. For datasets destined to MDS, a provider lists in its catalog only those whose assets conform ([Validation](#validation)). The vocabulary implements mobilityDCAT-AP and defines one term of its own, `manualApproval`, in `https://w3id.org/mobility-dataspace/2026/1/vocabulary/` ([MDS terms](#mds-terms)).

Prefixes:

| Prefix | Namespace |
|---|---|
| `dcat` | `http://www.w3.org/ns/dcat#` |
| `dct` | `http://purl.org/dc/terms/` |
| `owl` | `http://www.w3.org/2002/07/owl#` |
| `skos` | `http://www.w3.org/2004/02/skos/core#` |
| `adms` | `http://www.w3.org/ns/adms#` |
| `mobilitydcatap` | `https://w3id.org/mobilitydcat-ap/` |
| `mobilitydcatap-theme` | `https://w3id.org/mobilitydcat-ap/mobility-theme/` |
| `rdfs` | `http://www.w3.org/2000/01/rdf-schema#` |
| `mds-vocabulary` | `https://w3id.org/mobility-dataspace/2026/1/vocabulary/` |

## Accepted properties

An asset conforms to this vocabulary when it has every required property, has no property other than those listed here, at any nesting level, and its values follow [Mobility themes](#mobility-themes) and [Transport modes](#transport-modes). A provider's obligation is in [Validation](#validation).

### Required

A conforming asset has each of these properties.

| Property | IRI |
|---|---|
| `dct:title` | `http://purl.org/dc/terms/title` |
| `mobilitydcatap:mobilityTheme` → `mobilitydcatap-theme:data-content-category` | `https://w3id.org/mobilitydcat-ap/mobilityTheme` → `https://w3id.org/mobilitydcat-ap/mobility-theme/data-content-category` |

### Optional

| Property | IRI |
|---|---|
| `dct:description` | `http://purl.org/dc/terms/description` |
| `dct:language` | `http://purl.org/dc/terms/language` |
| `dct:publisher` | `http://purl.org/dc/terms/publisher` |
| `dct:license` | `http://purl.org/dc/terms/license` |
| `dct:rightsHolder` | `http://purl.org/dc/terms/rightsHolder` |
| `dct:accessRights` | `http://purl.org/dc/terms/accessRights` |
| `dct:isReferencedBy` | `http://purl.org/dc/terms/isReferencedBy` |
| `dct:accrualPeriodicity` | `http://purl.org/dc/terms/accrualPeriodicity` |
| `dcat:organization` | `http://www.w3.org/ns/dcat#organization` |
| `dcat:keywords` | `http://www.w3.org/ns/dcat#keywords` |
| `dcat:mediaType` | `http://www.w3.org/ns/dcat#mediaType` |
| `dcat:landingPage` | `http://www.w3.org/ns/dcat#landingPage` |
| `owl:versionInfo` | `http://www.w3.org/2002/07/owl#versionInfo` |
| `mobilitydcatap:transportMode` | `https://w3id.org/mobilitydcat-ap/transportMode` |
| `mobilitydcatap:georeferencingMethod` | `https://w3id.org/mobilitydcat-ap/georeferencingMethod` |
| `adms:sample` | `http://www.w3.org/ns/adms#sample` |
| `mobilitydcatap:mobilityTheme` → `mobilitydcatap-theme:data-content-sub-category` | `https://w3id.org/mobilitydcat-ap/mobilityTheme` → `https://w3id.org/mobilitydcat-ap/mobility-theme/data-content-sub-category` |
| `dct:spatial` → `skos:prefLabel` | `http://purl.org/dc/terms/spatial` → `http://www.w3.org/2004/02/skos/core#prefLabel` |
| `dct:spatial` → `dct:identifier` | `http://purl.org/dc/terms/spatial` → `http://purl.org/dc/terms/identifier` |
| `dct:temporal` → `dcat:startDate` | `http://purl.org/dc/terms/temporal` → `http://www.w3.org/ns/dcat#startDate` |
| `dct:temporal` → `dcat:endDate` | `http://purl.org/dc/terms/temporal` → `http://www.w3.org/ns/dcat#endDate` |
| `mobilitydcatap:mobilityDataStandard` → `@id` | `https://w3id.org/mobilitydcat-ap/mobilityDataStandard` → `@id` |
| `mobilitydcatap:mobilityDataStandard` → `mobilitydcatap:schema` → `dcat:downloadURL` | `https://w3id.org/mobilitydcat-ap/mobilityDataStandard` → `https://w3id.org/mobilitydcat-ap/schema` → `http://www.w3.org/ns/dcat#downloadURL` |
| `mobilitydcatap:mobilityDataStandard` → `mobilitydcatap:schema` → `rdfs:Literal` | `https://w3id.org/mobilitydcat-ap/mobilityDataStandard` → `https://w3id.org/mobilitydcat-ap/schema` → `http://www.w3.org/2000/01/rdf-schema#Literal` |
| `mds-vocabulary:manualApproval` | `https://w3id.org/mobility-dataspace/2026/1/vocabulary/manualApproval` |

## Validation

For datasets destined to MDS, a provider **MUST** list in its catalog only those whose assets conform to this vocabulary:

- an asset has required properties;
- an asset has only accepted properties, apart from `@type`;
- an asset's category, subcategory or transport mode is one of the values listed in [Mobility themes](#mobility-themes) and [Transport modes](#transport-modes).

*Note:* A MDS EDC connector rejects a non-conforming asset when it is created or updated. It does so in the EDC extension [`semantic-validator`](https://github.com/Mobility-Data-Space/mds-edc/tree/main/extensions/semantic-validator), as a Management API validator for `edc:Asset`.

## MDS terms

| Term | IRI | Values | Meaning |
|---|---|---|---|
| `manualApproval` | `https://w3id.org/mobility-dataspace/2026/1/vocabulary/manualApproval` | the string `true` or `false` | `true`: the provider approves each contract negotiation for this dataset by hand, so a negotiation may stay pending. Absent or `false`: negotiations are decided by the policy alone. |

The value of `manualApproval` is a string, not a JSON boolean, like the right operands of the MDS policies.

## Mobility themes

The mobility theme (`mobilitydcatap:mobilityTheme`) classifies a data offer by a category and, optionally, a subcategory of that category.

### Categories

`mobilitydcatap-theme:data-content-category` **MUST** be one of:

- `ROAD_EVENTS_AND_CONDITIONS`
- `ROAD_WORK_INFORMATION`
- `REAL_TIME_TRAFFIC_DATA`
- `PARKING_SERVICE_AND_REST_AREA_INFORMATION`
- `FILLING_AND_CHARGING_STATIONS`
- `DYNAMIC_TRAFFIC_SIGNS_AND_REGULATIONS`
- `STATIC_TRAFFIC_SIGNS_AND_REGULATIONS`
- `PUBLIC_TRANSPORT_SCHEDULED_TRANSPORT`
- `PUBLIC_TRANSPORT_NON_SCHEDULED_TRANSPORT`
- `SHARING_AND_HIRING_SERVICES`
- `CYCLE_NETWORK_DATA`
- `GENERAL_INFORMATION_FOR_TRIP-PLANNING`
- `STATIC_ROAD_NETWORK_DATA`
- `PEDESTRIAN_NETWORK_DATA`
- `TOLL_INFORMATION`
- `FREIGHT_AND_LOGISTICS`
- `AIR_AND_SPACE_TRAVEL`
- `WATERWAYS_AND_WATER_BODIES`
- `OTHER`

### Subcategories

`mobilitydcatap-theme:data-content-sub-category` **MUST** be one listed for the asset's category. A category without subcategories allows none.

| Category | Subcategories |
|---|---|
| `ROAD_EVENTS_AND_CONDITIONS` | `ACCIDENTS_AND_INCIDENTS`, `POOR_ROAD_CONDITIONS`, `ROAD_WEATHER_CONDITIONS`, `HAZARD_WARNINGS` |
| `ROAD_WORK_INFORMATION` | `LONG_TERM_ROAD_WORKS`, `SHORT_TERM_ROAD_WORKS` |
| `REAL_TIME_TRAFFIC_DATA` | `CURRENT_TRAVEL_TIME`, `EXPECTED_DELAYS`, `LOCATION_AND_LENGTH_OF_QUEUES`, `PREDICTED_TRAVEL_TIME`, `SPEED`, `TRAFFIC_DATA_AT_BORDER_CROSSINGS_TO_THIRD_COUNTRIES`, `TRAFFIC_VOLUME`, `WAITING_TIME_AT_BORDER_CROSSINGS_TO_NON-EU_MEMBER_STATES` |
| `PARKING_SERVICE_AND_REST_AREA_INFORMATION` | `BIKE_PARKING_LOCATIONS`, `CAR_PARKING_AVAILABILITY`, `CAR_PARKING_LOCATIONS_AND_CONDITIONS`, `PARK_AND_RIDE_STOPS`, `SERVICE_AND_REST_AREA_AVAILABILITY`, `SERVICE_AND_REST_AREA_LOCATIONS_AND_CONDITIONS`, `TRUCK_PARKING_AVAILABILITY`, `TRUCK_PARKING_LOCATIONS_AND_CONDITIONS` |
| `FILLING_AND_CHARGING_STATIONS` | `AVAILABILITY_OF_CHARGING_POINTS_FOR_ELECTRIC_VEHICLES`, `LOCATION_AND_CONDITIONS_OF_CHARGING_POINTS`, `AVAILABILITY_OF_FILLING_STATIONS`, `LOCATION_AND_CONDITIONS_OF_FILLING_STATIONS` |
| `DYNAMIC_TRAFFIC_SIGNS_AND_REGULATIONS` | `BRIDGE_CLOSURES_AND_ACCESS_CONDITIONS`, `DIRECTION_OF_TRAVEL_ON_REVERSIBLE_LANES`, `DYNAMIC_OVERTAKING_BANS_ON_HEAVY_GOODS_VEHICLES`, `DYNAMIC_SPEED_LIMITS`, `LANE_CLOSURES_AND_ACCESS_CONDITIONS`, `OTHER_ACCESS_RESTRICTIONS_AND_TRAFFIC_REGULATIONS`, `OTHER_TEMPORARY_TRAFFIC_MANAGEMENT_MEASURES_OR_PLANS`, `ROAD_CLOSURES_AND_ACCESS_CONDITIONS`, `TUNNEL_CLOSURES_AND_ACCESS_CONDITIONS` |
| `STATIC_TRAFFIC_SIGNS_AND_REGULATIONS` | `BRIDGE_ACCESS_CONDITIONS`, `OTHER_STATIC_TRAFFIC_SIGNS`, `OTHER_TRAFFIC_REGULATIONS`, `PERMANENT_ACCESS_RESTRICTIONS`, `SPEED_LIMITS`, `TRAFFIC_CIRCULATION_PLANS`, `TUNNEL_ACCESS_CONDITIONS` |
| `PUBLIC_TRANSPORT_SCHEDULED_TRANSPORT` | `BASIC_COMMERCIAL_CONDITIONS`, `BASIC_COMMON_STANDARD_FARES`, `COMMON_FARE_PRODUCTS`, `CONNECTION_LINKS`, `DISRUPTIONS_DELAYS_CANCELLATIONS`, `ENVIRONMENTAL_STANDARDS_FOR_VEHICLES`, `HOURS_OF_OPERATION`, `NETWORK_TOPOLOGY_AND_ROUTES_LINES`, `OPERATIONAL_CALENDAR`, `PASSENGER_CLASSES`, `PLANNED_INTERCHANGES_BETWEEN_SCHEDULED_SERVICES`, `PURCHASE_INFORMATION`, `REAL_TIME_ESTIMATED_DEPARTURE_AND_ARRIVAL_TIMES`, `SPECIAL_FARE_PRODUCTS`, `STOP_FACILITIES_ACCESSIBILITY_AND_PATHS_WITHIN_FACILITY`, `STOP_FACILITIES_GEOMETRY_AND_MAP_LAYOUT`, `STOP_FACILITIES_LOCATION_AND_FEATURES`, `STOP_FACILITIES_STATUS_OF_FEATURES`, `TIMETABLES_STATIC`, `TRANSPORT_OPERATORS`, `VEHICLE_DETAILS` |
| `PUBLIC_TRANSPORT_NON_SCHEDULED_TRANSPORT` | `ACCESIBILITY_INFORMATION_FOR_VEHICLES`, `ENVIRONMENTAL_STANDARDS_FOR_VEHICLES`, `FARES`, `LOCATIONS_AND_STATIONS`, `PROVIDER_DATA`, `RESERVATION_AND_PURCHASE_OPTIONS`, `SERVICE_AREAS_AND_SERVICE_TIMES` |
| `SHARING_AND_HIRING_SERVICES` | `BIKE_HIRING_AVAILABILITY`, `BIKE_HIRING_STATIONS`, `BIKE_SHARING_AVAILABILITY`, `BIKE_SHARING_LOCATIONS_AND_STATIONS`, `CAR_HIRING_STATIONS`, `CAR_HIRING_AVAILABILITY`, `CAR_SHARING_AVAILABILITY`, `CAR_SHARING_LOCATIONS_AND_STATIONS`, `ENVIRONMENTAL_STANDARDS_FOR_VEHICLES`, `E_SCOOTER_SHARING_AVAILABILITY`, `E_SCOOTER_SHARING_LOCATIONS_AND_STATIONS`, `PAYMENT_METHODS` |
| `CYCLE_NETWORK_DATA` | `NETWORK_CLOSURES_DIVERSIONS`, `NETWORK_DETAILED_ATTRIBUTES`, `NETWORK_GEOMETRY_AND_LANE_CHARACTER` |
| `GENERAL_INFORMATION_FOR_TRIP-PLANNING` | `ADDRESS_IDENTIFIERS`, `PARAMETERS_NEEDED_TO_CALCULATE_COSTS`, `PARAMETERS_NEEDED_TO_CALCULATE_ENVIRONMENTAL_FACTORS`, `POINTS_OF_INTERESTS`, `TOPOGRAPHIC_PLACES` |
| `STATIC_ROAD_NETWORK_DATA` | `GEOMETRY`, `GRADIENTS`, `JUNCTIONS`, `NUMBER_OF_LANES`, `ROAD_CLASSIFICATION`, `ROAD_WIDTH` |
| `PEDESTRIAN_NETWORK_DATA` | `PEDESTRIAN_ACCESSIBILITY_FACILITIES`, `PEDESTRIAN_NETWORK_GEOMETRY` |
| `TOLL_INFORMATION` | `APPLICABLE_ROAD_USER_CHARGES_AND_PAYMENT_METHODS`, `IDENTIFICATION_OF_TOLLED_ROADS`, `LOCATION_OF_TOLLING_STATIONS`, `PAYMENT_METHODS_FOR_TOLLS` |
| `FREIGHT_AND_LOGISTICS` | `AVAILABILITY_OF_DELIVERY_AREAS`, `FREIGHT_DELIVERY_REGULATIONS`, `LOCATION_OF_DELIVERY_AREAS` |
| `AIR_AND_SPACE_TRAVEL` | none |
| `WATERWAYS_AND_WATER_BODIES` | none |
| `OTHER` | none |

## Transport modes

`mobilitydcatap:transportMode` **MUST** be one of:

- `AIR`
- `BICYCLE`
- `BIKE_HIRE`
- `BIKE_SHARING`
- `BUS`
- `CAR`
- `CAR_HIRE`
- `CAR_POOLING`
- `CAR_SHARING`
- `E_SCOOTER`
- `LONG_DISTANCE_COACH`
- `LONG_DISTANCE_RAIL`
- `MARITIME`
- `METRO_SUBWAY_TRAIN`
- `MOTORCYCLE`
- `OTHER`
- `PEDESTRIAN`
- `REGIONAL_AND_LOCAL_RAIL`
- `RIDE_POOLING`
- `SHUTTLE_BUS`
- `SHUTTLE_FERRY`
- `TAXI`
- `TRAM_LIGHT_RAIL`
- `TRUCK`
