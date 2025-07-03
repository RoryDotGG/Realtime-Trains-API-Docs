# Pull API Documentation - Service Information

## Endpoint

```
/json/service/<serviceUid>/<year>/<month>/<day>
```

## Parameters

| Parameter | Details |
|-----------|---------|
| `serviceUid` (required) | Service UID, as obtained from a location search |
| `date` (required) | In format yyyy/mm/dd, example: 2013/06/14 |

## Output Values

### Service

| Parameter | Default | Details |
|-----------|---------|---------|
| `serviceUid` | - | Contains the service identifier for this service, paired with the run date this will always be a unique identifier. Service UIDs use the following regex pattern `[A-Z][0-9]{5}`. |
| `runDate` | - | Contains the running date of this service, based on its departure time from the first origin. In format YYYY-MM-DD. |
| `serviceType` | - | Contains the type of service this is, bus, ship or train. |
| `isPassenger` | - | boolean output determining whether the service is a passenger service or not |
| `trainIdentity` | detailed | The train identity that this service was planned to run to. FOC operated services will always show as FRGT. |
| `powerType` | detailed | The power type of the service. This is as described in the Network Rail CIF documentation. |
| `trainClass` | null | The classes that this service conveys. This is as described in the Network Rail CIF documentation. If the field is blank and is a passenger train, the train conveys first and standard class accommodation only. |
| `sleeper` | null | The types of sleeper that this service conveys. This is as described in the Network Rail CIF documentation. |
| `atocCode` | ZZ | The two character identifier, as used by ATOC, to identify the service operator, example: SW |
| `atocName` | Unknown | Service operator, example: South West Trains |
| `performanceMonitored` | - | boolean output detailing whether the service is subject to PPM (Public Performance Measurement) monitoring. |
| `origin` | - | Array of Pair objects forming the overall origins of the service, detailed further down. |
| `destination` | - | Array of Pair objects forming the overall destination of the service, detailed further down. |
| `locations` | - | Array of Location objects forming the locations that the service calls at (and, in detailed, passes). |
| `realtimeActivated` | false | Details whether this service has been activated for realtime information |
| `runningIdentity` | - | This field appears if realtimeActivated is set as true. It identifies the current running identity of the service. |

### Pair

| Parameter | Default | Details |
|-----------|---------|---------|
| `tiploc` | detailed | TIPLOC of the relevant location, example: WATRLMN |
| `description` | - | Text name of the relevant location, example: London Waterloo |
| `workingTime` | detailed | Relevant working time for this location for the activity that this pair is performing. If it is in the context of an origin, it will be a departure time - for a destination it will be an arrival time. In format HHmmss, example: 150330. |
| `publicTime` | - | As workingTime but for the advertised public times. In format HHmm, example: 1503. |

### Location

| Parameter | Default | Details |
|-----------|---------|---------|
| `realtimeActivated` | false | Details whether this service has been activated for realtime information |
| `tiploc` | - | TIPLOC code for the location, example: WATRLMN |
| `crs` | null | CRS code for the location, example: WAT |
| `description` | - | Text name of the relevant location, example: London Waterloo |
| `wttBookedArrival` | null | Working Timetable arrival time of the service at this location, in format HHmmss |
| `wttBookedDeparture` | null | Working Timetable departure time of the service at this location, in format HHmmss |
| `wttBookedPass` | null | Working Timetable passing time of the service at this location, in format HHmmss |
| `gbttBookedArrival` | null | Public Timetable arrival time of the service at this location, in format HHmm |
| `gbttBookedDeparture` | null | Public Timetable departure time of the service at this location, in format HHmm |
| `origin` | - | Array of Pair objects forming the origin of the service as at this location |
| `destination` | - | Array of Pair objects forming the destination of the service as at this location |
| `isCall` | false | boolean output as to whether this service calls at this location. This is set as true even if the service ends up non-stopping this station for whatever reason. |
| `isCallPublic` | false | boolean output as to whether this service makes a public call at this location. This is set as true even if the service ends up non-stopping this station for whatever reason. |
| `realtimeArrival` | null | Expected or actual arrival time of this service, in format HHmm |
| `realtimeArrivalActual` | false | Always appears if realtimeArrival is also present. Boolean output stating whether this is an actual or expected time. If true, actual - if false, expected. |
| `realtimeArrivalNoReport` | false | If set as true, this means that the train has already arrived at this station but no report was received, and a later one has been |
| `realtimeWttArrivalLateness` | 0 | If the service has an actual time, a lateness in minutes will be provided based from the WTT time. Positive values mean the service was late, negative values mean the service was early. |
| `realtimeGbttArrivalLateness` | 0 | If the service has an actual time, a lateness in minutes will be provided based from the public timetable time. Positive values mean the service was late, negative values mean the service was early. |
| `realtimeDeparture` | null | Expected or actual departure time of this service, in format HHmm |
| `realtimeDepartureActual` | false | Always appears if realtimeDeparture is also present. Boolean output stating whether this is an actual or expected time. If true, actual - if false, expected. |
| `realtimeDepartureNoReport` | false | If set as true, this means that the train has already departed this station but no report was received, and a later one has been |
| `realtimeWttDepartureLateness` | 0 | If the service has an actual time, a lateness in minutes will be provided based from the WTT time. Positive values mean the service was late, negative values mean the service was early. |
| `realtimeGbttDepartureLateness` | 0 | If the service has an actual time, a lateness in minutes will be provided based from the public timetable time. Positive values mean the service was late, negative values mean the service was early. |
| `realtimePass` | null | Expected or actual passing time of this service, in format HHmm |
| `realtimePassActual` | false | Always appears if realtimePass is also present. Boolean output stating whether this is an actual or expected time. If true, actual - if false, expected. |
| `realtimePassNoReport` | false | If set as true, this means that the train has already passed this station but no report was received, and a later one has been |
| `realtimeWttArrivalLateness` | 0 | If the service has an actual time, a lateness in minutes will be provided based from the WTT time. Positive values mean the service was late, negative values mean the service was early. |
| `platform` | none | The expected platform that this service will use at this location |
| `platformConfirmed` | false | boolean output - if this is set to true, then the service has used/will use the platform stated |
| `platformChanged` | false | boolean output - if this is set to true, then the service has changed from the planned platform |
| `line` | none | The expected line that this service will use at this location |
| `lineConfirmed` | false | boolean output - if this is set to true, then the service has used/will use the line stated |
| `path` | none | The expected path that this service will use at this location |
| `pathConfirmed` | false | boolean output - if this is set to true, then the service has used/will use the path stated |
| `cancelReasonCode` | null | If this service is cancelled at this location, this will be populated with a two character cancellation code which can be cross-referenced with the Delay Attribution Guide. |
| `cancelReasonShortText` | null | Short text reason detailing the reason for the cancellation |
| `cancelReasonLongText` | null | Long text reason detailing the reason for the cancellation |
| `displayAs` | - | Values that can appear in this field are CALL, PASS, ORIGIN, DESTINATION, STARTS, TERMINATES, CANCELLED_CALL, CANCELLED_PASS. ORIGIN and DESTINATION represent the original origin & destination of a service. If STARTS or TERMINATES appear, then this means a service has started short or terminated en-route - the original origin/destination will show CANCELLED_CALL. |
| `serviceLocation` | null | Values that can appear in this field are APPR_STAT (Approaching Station), APPR_PLAT (Arriving), AT_PLAT (At Platform, as referenced in platform), DEP_PREP (Preparing to depart) and DEP_READY (Ready to depart). |

## Errors

If the requested service cannot be found, a HTTP 404 will be returned.

## Example

The following example contains all fields that may appear in an output, and does not deal with the separation between simple and detailed views.

```json
{
    "serviceUid": "W72419",
    "runDate": "2013-06-11",
    "serviceType": "train",
    "isPassenger": true,
    "trainIdentity": "2A61",
    "powerType": "EMU",
    "trainClass": "B",
    "atocCode": "SN",
    "atocName": "Southern",
    "performanceMonitored": true,
    "origin": [
        {
            "tiploc": "BRGHTN",
            "description": "Brighton",
            "workingTime": "230500",
            "publicTime": "2305"
        }
    ],
    "destination": [
        {
            "tiploc": "VICTRIC",
            "description": "London Victoria",
            "workingTime": "003900",
            "publicTime": "0039"
        }
    ],
    "locations": [
        {
            "realtimeActivated": true,
            "tiploc": "BRGHTN",
            "crs": "BTN",
            "description": "Brighton",
            "wttBookedDeparture": "230500",
            "gbttBookedDeparture": "2305",
            "origin": [
                {
                    "tiploc": "BRGHTN",
                    "description": "Brighton",
                    "workingTime": "230500",
                    "publicTime": "2305"
                }
            ],
            "destination": [
                {
                    "tiploc": "VICTRIC",
                    "description": "London Victoria",
                    "workingTime": "003900",
                    "publicTime": "0039"
                }
            ],
            "isCall": true,
            "isPublicCall": true,
            "realtimeDeparture": "2304",
            "realtimeDepartureActual": true,
            "realtimeGbttDepartureLateness": null,
            "platform": "6",
            "platformConfirmed": true,
            "platformChanged": false,
            "line": "M",
            "lineConfirmed": true,
            "displayAs": "ORIGIN"
        },
        {
            "realtimeActivated": true,
            "tiploc": "ECROYDN",
            "crs": "ECR",
            "description": "East Croydon",
            "wttBookedArrival": "001700",
            "wttBookedDeparture": "001800",
            "gbttBookedArrival": "0017",
            "gbttBookedDeparture": "0018",
            "origin": [
                {
                    "tiploc": "BRGHTN",
                    "description": "Brighton",
                    "workingTime": "230500",
                    "publicTime": "2305"
                }
            ],
            "destination": [
                {
                    "tiploc": "VICTRIC",
                    "description": "London Victoria",
                    "workingTime": "003900",
                    "publicTime": "0039"
                }
            ],
            "isCall": true,
            "isPublicCall": true,
            "realtimeArrival": "0017",
            "realtimeArrivalActual": true,
            "realtimeDeparture": "0018",
            "realtimeDepartureActual": true,
            "platform": "4",
            "platformConfirmed": true,
            "platformChanged": false,
            "line": "S",
            "lineConfirmed": true,
            "displayAs": "CALL"
        },
        {
            "realtimeActivated": true,
            "tiploc": "CLPHMJC",
            "crs": "CLJ",
            "description": "Clapham Junction",
            "wttBookedArrival": "003100",
            "wttBookedDeparture": "003200",
            "gbttBookedArrival": "0031",
            "gbttBookedDeparture": "0032",
            "origin": [
                {
                    "tiploc": "BRGHTN",
                    "description": "Brighton",
                    "workingTime": "230500",
                    "publicTime": "2305"
                }
            ],
            "destination": [
                {
                    "tiploc": "VICTRIC",
                    "description": "London Victoria",
                    "workingTime": "003900",
                    "publicTime": "0039"
                }
            ],
            "isCall": true,
            "isPublicCall": true,
            "realtimeArrival": "0033",
            "realtimeArrivalActual": false,
            "realtimeDeparture": "0034",
            "realtimeDepartureActual": false,
            "platform": "14",
            "platformConfirmed": false,
            "platformChanged": false,
            "line": "SL",
            "lineConfirmed": false,
            "serviceLocation": "APPR_STAT",
            "displayAs": "CALL"
        },
        {
            "realtimeActivated": true,
            "tiploc": "VICTRIC",
            "crs": "VIC",
            "description": "London Victoria",
            "wttBookedArrival": "003900",
            "gbttBookedArrival": "0039",
            "origin": [
                {
                    "tiploc": "BRGHTN",
                    "description": "Brighton",
                    "workingTime": "230500",
                    "publicTime": "2305"
                }
            ],
            "destination": [
                {
                    "tiploc": "VICTRIC",
                    "description": "London Victoria",
                    "workingTime": "003900",
                    "publicTime": "0039"
                }
            ],
            "isCall": true,
            "isPublicCall": true,
            "realtimeArrival": "0041",
            "realtimeArrivalActual": false,
            "platform": "15",
            "platformConfirmed": false,
            "platformChanged": false,
            "displayAs": "DESTINATION"
        }
    ],
    "realtimeActivated": true,
    "runningIdentity": "2A61"
}
```
