# Pull API Documentation - Location Line-Up

## Endpoints

### Normal queries (live departures)
```
/json/search/<station>
```

### Normal queries filtered to a location
```
/json/search/<station>/to/<toStation>
```

### Queries for all services on a specific date
```
/json/search/<station>/<year>/<month>/<day>
```

### Queries for services on a specific date and time
```
/json/search/<station>/<year>/<month>/<day>/<time>
```

**Note:** You can append `/arrivals` to any of these endpoints to retrieve info about arrivals. You can apply the to/from filtering to any of the endpoints, they must be before any date/time modifiers.

## Parameters

| Parameter | Details |
|-----------|---------|
| `station` (required) | CRS or TIPLOC |
| `toStation` (optional) | CRS or TIPLOC |
| `date` (optional) | In format yyyy/mm/dd, example: 2013/06/14 |
| `time` (optional) | In format hhmm, example: 0810 or 2315 |

## Output Values

### Container

| Parameter | Default | Details |
|-----------|---------|---------|
| `location` | - | LocationDetail object detailing the location searched for |
| `filter` | null | LocationDetail objects detailing the location searched for, nested within from & to properties |
| `services` | - | Array of LocationContainer containing the location information and service metadata |

### Location Container

| Parameter | Default | Details |
|-----------|---------|---------|
| `locationDetail` | - | Contains the Location object containing details about the location itself, details below. |
| `serviceUid` | - | Contains the service identifier for this service, paired with the run date this will always be a unique identifier. Service UIDs use the following regex pattern `[A-Z][0-9]{5}`. |
| `runDate` | - | Contains the running date of this service, based on its departure time from the first origin. In format YYYY-MM-DD. |
| `trainIdentity` | detailed | The train identity that this service was planned to run to. FOC operated services will always show as FRGT. |
| `runningIdentity` | as previous | Identifies the current running identity of the service. |
| `atocCode` | ZZ | The two character identifier, as used by ATOC, to identify the service operator, example: SW |
| `atocName` | Unknown | Service operator, example: South West Trains |
| `serviceType` | - | Contains the type of service this is, bus, ship or train. |
| `isPassenger` | - | boolean output determining whether the service is a passenger service or not |
| `plannedCancel` | false | boolean output determining whether this service was a planned cancellation. A planned cancellation is one not advertised, at all, for operation on that day and a service with this should be disregarded - it is the equivalent of the STP indicator 'C'. |
| `origin` | - | Array of Pair objects forming the overall origins of the service, detailed further down. Only appears if the service has experienced an en-route cancellation. |
| `destination` | - | Array of Pair objects forming the overall destinations of the service, detailed further down. Only appears if the service has experienced an en-route cancellation. |
| `countdownMinutes` | - | Number of minutes until expected departures, currently present only on 'high frequency' metro services - operated by London Overground and Merseyrail. |

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
| `realtimeGbttDepartureLateness` | 0 | If the service has an actual time, a lateness in minutes will be provided based from the public timetable time. Positive values mean the service was late, negative values mean the service were early. |
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
   "location": {
       "name": "Bournemouth",
       "crs": "BMH",
       "tiploc": "BOMO"
   },
   "filter": null,
   "services": [
       {
           "locationDetail": {
               "realtimeActivated": true,
               "tiploc": "BOMO",
               "crs": "BMH",
               "description": "Bournemouth",
               "wttBookedArrival": "011630",
               "wttBookedDeparture": "011830",
               "gbttBookedArrival": "0117",
               "gbttBookedDeparture": "0118",
               "origin": [
                   {
                       "tiploc": "WATRLMN",
                       "description": "London Waterloo",
                       "workingTime": "230500",
                       "publicTime": "2305"
                   }
               ],
               "destination": [
                   {
                       "tiploc": "POOLE",
                       "description": "Poole",
                       "workingTime": "013000",
                       "publicTime": "0130"
                   }
               ],
               "isCall": true,
               "isPublicCall": true,
               "realtimeArrival": "0114",
               "realtimeArrivalActual": false,
               "realtimeDeparture": "0118",
               "realtimeDepartureActual": false,
               "platform": "3",
               "platformConfirmed": false,
               "platformChanged": false,
               "displayAs": "CALL"
           },
           "serviceUid": "W90091",
           "runDate": "2013-06-11",
           "trainIdentity": "1B77",
           "runningIdentity": "1B77",
           "atocCode": "SW",
           "atocName": "South West Trains",
           "serviceType": "train",
           "isPassenger": true
       }
   ]
}
```
