
# TrafficMode

Defines how to consider traffic in a matrix calculation. * `CONSTANT` - Use the constant **travelTime** for the selected vehicle.   Traffic conditions are assumed to be steady, unaffected by rush hours, events, or other temporary changes in congestion.                    If **startTime** is specified, it will only affect toll calculation. * `AVERAGE` - Use the average **travelTime** for the selected vehicle.  If **startTime** is specified, the typical traffic situation for that time of day and day of week will be considered such as rush hours  on Monday morning or light traffic on Saturday evening. Toll will be calculated according to that date and time. * `REALISTIC` - Use the most realistic **travelTime** for the selected vehicle and the  given **startTime**.  Takes into account the live traffic situation such as traffic jams or road works  as well as the typical traffic situation at the time of day and the day of week of travel such as rush hours  on Monday morning or light traffic on Saturday evening.  See [here](./concepts/time-dependent-matrix) for more information.

## Properties

Name | Type
------------ | -------------

## Example

```typescript
import type { TrafficMode } from ''

// TODO: Update the object below with actual values
const example = {
} satisfies TrafficMode

console.log(example)

// Convert the instance to a JSON string
const exampleJSON: string = JSON.stringify(example)
console.log(exampleJSON)

// Parse the JSON string back to an object
const exampleParsed = JSON.parse(exampleJSON) as TrafficMode
console.log(exampleParsed)
```

[[Back to top]](#) [[Back to API list]](../README.md#api-endpoints) [[Back to Model list]](../README.md#models) [[Back to README]](../README.md)


