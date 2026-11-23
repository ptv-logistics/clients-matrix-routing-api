
# ResultFormat

Defines the format for the distances, travel times, toll costs, directDistance flags and violation flags in the response. Note that the encoded format should be selected if **startTime** and **duration** are set.    * `PLAIN` - Values are returned as plain arrays.    * `ENCODED` - Values are returned as encoded arrays.

## Properties

Name | Type
------------ | -------------

## Example

```typescript
import type { ResultFormat } from ''

// TODO: Update the object below with actual values
const example = {
} satisfies ResultFormat

console.log(example)

// Convert the instance to a JSON string
const exampleJSON: string = JSON.stringify(example)
console.log(exampleJSON)

// Parse the JSON string back to an object
const exampleParsed = JSON.parse(exampleJSON) as ResultFormat
console.log(exampleParsed)
```

[[Back to top]](#) [[Back to API list]](../README.md#api-endpoints) [[Back to Model list]](../README.md#models) [[Back to README]](../README.md)


