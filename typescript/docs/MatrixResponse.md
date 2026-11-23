
# MatrixResponse


## Properties

Name | Type
------------ | -------------
`percentageOfDirectDistanceRelations` | number
`distances` | Array&lt;number&gt;
`distancesEncoded` | string
`travelTimes` | Array&lt;number&gt;
`travelTimesEncoded` | string
`travelTimeProfilesEncoded` | string
`tollCosts` | Array&lt;number&gt;
`tollCostsEncoded` | string
`directDistanceFlags` | Array&lt;boolean&gt;
`directDistanceFlagsEncoded` | string
`violationFlags` | Array&lt;boolean&gt;
`violationFlagsEncoded` | string
`warnings` | [Array&lt;Warning&gt;](Warning.md)

## Example

```typescript
import type { MatrixResponse } from ''

// TODO: Update the object below with actual values
const example = {
  "percentageOfDirectDistanceRelations": null,
  "distances": null,
  "distancesEncoded": null,
  "travelTimes": null,
  "travelTimesEncoded": null,
  "travelTimeProfilesEncoded": null,
  "tollCosts": null,
  "tollCostsEncoded": null,
  "directDistanceFlags": null,
  "directDistanceFlagsEncoded": null,
  "violationFlags": null,
  "violationFlagsEncoded": null,
  "warnings": null,
} satisfies MatrixResponse

console.log(example)

// Convert the instance to a JSON string
const exampleJSON: string = JSON.stringify(example)
console.log(exampleJSON)

// Parse the JSON string back to an object
const exampleParsed = JSON.parse(exampleJSON) as MatrixResponse
console.log(exampleParsed)
```

[[Back to top]](#) [[Back to API list]](../README.md#api-endpoints) [[Back to Model list]](../README.md#models) [[Back to README]](../README.md)


