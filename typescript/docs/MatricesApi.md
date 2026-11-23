# MatricesApi

All URIs are relative to *https://api.myptv.com/matrixrouting/v1*

| Method | HTTP request | Description |
|------------- | ------------- | -------------|
| [**calculateMatrix**](MatricesApi.md#calculatematrix) | **POST** /matrices |  |
| [**cancelMatrixCalculation**](MatricesApi.md#cancelmatrixcalculation) | **DELETE** /matrices/{id} |  |
| [**getMatrix**](MatricesApi.md#getmatrix) | **GET** /matrices/{id} |  |
| [**getRouteId**](MatricesApi.md#getrouteid) | **POST** /matrices/route |  |
| [**getStatus**](MatricesApi.md#getstatus) | **GET** /matrices/status/{id} |  |
| [**startMatrixCalculation**](MatricesApi.md#startmatrixcalculation) | **POST** /matrices/async |  |



## calculateMatrix

> MatrixResponse calculateMatrix(locations, profile, results, options)



Creates a matrix by calculating distances and travel times between given origins and destinations. \\ The request is rejected if the number of origins or the number of destinations is greater than 10,000 or the number of relations (number of origins * number of destinations) is greater than 250,000.\\ The &#x60;TOLL_COSTS&#x60; result option is not allowed with this operation because toll cost calculation takes much longer. \\ Gzip-encoded content is supported in the request body and returned in the response if accepted by the client.\\ Please use the startMatrixCalculation operation * if you want to get toll costs, * for time-dependent matrices returning travel time profiles, * for more origins, destinations and relations (see also the [FAQ](../../help/faq-help) for details regarding limits).

### Example

```ts
import {
  Configuration,
  MatricesApi,
} from '';
import type { CalculateMatrixRequest } from '';

async function example() {
  console.log("🚀 Testing  SDK...");
  const config = new Configuration({ 
    // To configure API key authorization: apiKeyAuth
    apiKey: "YOUR API KEY",
  });
  const api = new MatricesApi(config);

  const body = {
    // Locations
    locations: ...,
    // string | A profile defines a vehicle by a set of attributes, matching typical transport situations. It must be the name of one of the [predefined profiles](./concepts/profiles-and-countries) such as _EUR_TRAILER_TRUCK_. (optional)
    profile: profile_example,
    // Array<Results> | Comma-separated list that defines which results will be returned.  * `DISTANCES`     Response includes information about the distances between start and destination locations.  * `TRAVEL_TIMES`     Response includes information about the travel times between start and destination locations.  * `TOLL_COSTS`     Response includes information about the toll costs between start and destination locations.     Toll tariffs are evaluated based on the date and time specified in `options[tollTime]` when `options[trafficMode]` is set to _AVERAGE_ or `options[startTime]` when `options[trafficMode]` is set to _CONSTANT_.     If no date and time are provided, tolls are calculated using the tariffs valid at noon on Monday of the current week.     For custom routing profiles, the UTC offset is derived from the profile\'s timezone setting, accounting for daylight saving time.     For predefined profiles, a representative timezone for the profile\'s region is used:     * _EUROPE_ - Central European Time / Central European Summer Time (UTC+01:00/+02:00)     * _AMERICA_ - Central Time (UTC-06:00/-05:00)     * _IMEA_ - Arabia Standard Time (UTC+03:00)     * _AUSTRALIA_ - Australian Eastern Time (UTC+10:00/+11:00)     * _WORLD_ - UTC (+00:00)      **Only available for startMatrixCalculation operation.**  * `DIRECT_DISTANCE_FLAGS`     Response includes flags describing if relations have been estimated by direct distance.  * `VIOLATION_FLAGS`     Response includes flags describing if relations contain violations. (optional)
    results: ["TRAVEL_TIMES"],
    // Options | Matrix Routing-relevant options like the currency for the toll costs. Use array notation like `options[currency]=EUR` to set options. (optional)
    options: ...,
  } satisfies CalculateMatrixRequest;

  try {
    const data = await api.calculateMatrix(body);
    console.log(data);
  } catch (error) {
    console.error(error);
  }
}

// Run the test
example().catch(console.error);
```

### Parameters


| Name | Type | Description  | Notes |
|------------- | ------------- | ------------- | -------------|
| **locations** | [Locations](Locations.md) |  | |
| **profile** | `string` | A profile defines a vehicle by a set of attributes, matching typical transport situations. It must be the name of one of the [predefined profiles](./concepts/profiles-and-countries) such as _EUR_TRAILER_TRUCK_. | [Optional] [Defaults to `&#39;EUR_TRAILER_TRUCK&#39;`] |
| **results** | `Array<Results>` | Comma-separated list that defines which results will be returned.  * &#x60;DISTANCES&#x60;     Response includes information about the distances between start and destination locations.  * &#x60;TRAVEL_TIMES&#x60;     Response includes information about the travel times between start and destination locations.  * &#x60;TOLL_COSTS&#x60;     Response includes information about the toll costs between start and destination locations.     Toll tariffs are evaluated based on the date and time specified in &#x60;options[tollTime]&#x60; when &#x60;options[trafficMode]&#x60; is set to _AVERAGE_ or &#x60;options[startTime]&#x60; when &#x60;options[trafficMode]&#x60; is set to _CONSTANT_.     If no date and time are provided, tolls are calculated using the tariffs valid at noon on Monday of the current week.     For custom routing profiles, the UTC offset is derived from the profile\&#39;s timezone setting, accounting for daylight saving time.     For predefined profiles, a representative timezone for the profile\&#39;s region is used:     * _EUROPE_ - Central European Time / Central European Summer Time (UTC+01:00/+02:00)     * _AMERICA_ - Central Time (UTC-06:00/-05:00)     * _IMEA_ - Arabia Standard Time (UTC+03:00)     * _AUSTRALIA_ - Australian Eastern Time (UTC+10:00/+11:00)     * _WORLD_ - UTC (+00:00)      **Only available for startMatrixCalculation operation.**  * &#x60;DIRECT_DISTANCE_FLAGS&#x60;     Response includes flags describing if relations have been estimated by direct distance.  * &#x60;VIOLATION_FLAGS&#x60;     Response includes flags describing if relations contain violations. | [Optional] |
| **options** | [](.md) | Matrix Routing-relevant options like the currency for the toll costs. Use array notation like &#x60;options[currency]&#x3D;EUR&#x60; to set options. | [Optional] [Defaults to `undefined`] |

### Return type

[**MatrixResponse**](MatrixResponse.md)

### Authorization

[apiKeyAuth](../README.md#apiKeyAuth)

### HTTP request headers

- **Content-Type**: `application/json`
- **Accept**: `application/json`


### HTTP response details
| Status code | Description | Response headers |
|-------------|-------------|------------------|
| **200** | Response on success. |  -  |
| **0** | Response on failure. |  -  |

[[Back to top]](#) [[Back to API list]](../README.md#api-endpoints) [[Back to Model list]](../README.md#models) [[Back to README]](../README.md)


## cancelMatrixCalculation

> cancelMatrixCalculation(id)



Cancels a matrix calculation and deletes the calculated results specified by its ID. Results already calculated cannot be requested by its ID, anymore.

### Example

```ts
import {
  Configuration,
  MatricesApi,
} from '';
import type { CancelMatrixCalculationRequest } from '';

async function example() {
  console.log("🚀 Testing  SDK...");
  const config = new Configuration({ 
    // To configure API key authorization: apiKeyAuth
    apiKey: "YOUR API KEY",
  });
  const api = new MatricesApi(config);

  const body = {
    // string | The ID of a matrix calculation operation.
    id: 38400000-8cf0-11bd-b23e-10b96e4ef00d,
  } satisfies CancelMatrixCalculationRequest;

  try {
    const data = await api.cancelMatrixCalculation(body);
    console.log(data);
  } catch (error) {
    console.error(error);
  }
}

// Run the test
example().catch(console.error);
```

### Parameters


| Name | Type | Description  | Notes |
|------------- | ------------- | ------------- | -------------|
| **id** | `string` | The ID of a matrix calculation operation. | [Defaults to `undefined`] |

### Return type

`void` (Empty response body)

### Authorization

[apiKeyAuth](../README.md#apiKeyAuth)

### HTTP request headers

- **Content-Type**: Not defined
- **Accept**: `application/json`


### HTTP response details
| Status code | Description | Response headers |
|-------------|-------------|------------------|
| **204** | Response on success. |  -  |
| **0** | Response on failure. |  -  |

[[Back to top]](#) [[Back to API list]](../README.md#api-endpoints) [[Back to Model list]](../README.md#models) [[Back to README]](../README.md)


## getMatrix

> MatrixResponse getMatrix(id)



Requests the results of a matrix calculation operation. Gzip-encoded content is returned in the response if accepted by the client.

### Example

```ts
import {
  Configuration,
  MatricesApi,
} from '';
import type { GetMatrixRequest } from '';

async function example() {
  console.log("🚀 Testing  SDK...");
  const config = new Configuration({ 
    // To configure API key authorization: apiKeyAuth
    apiKey: "YOUR API KEY",
  });
  const api = new MatricesApi(config);

  const body = {
    // string | The ID of a matrix calculation operation.
    id: 38400000-8cf0-11bd-b23e-10b96e4ef00d,
  } satisfies GetMatrixRequest;

  try {
    const data = await api.getMatrix(body);
    console.log(data);
  } catch (error) {
    console.error(error);
  }
}

// Run the test
example().catch(console.error);
```

### Parameters


| Name | Type | Description  | Notes |
|------------- | ------------- | ------------- | -------------|
| **id** | `string` | The ID of a matrix calculation operation. | [Defaults to `undefined`] |

### Return type

[**MatrixResponse**](MatrixResponse.md)

### Authorization

[apiKeyAuth](../README.md#apiKeyAuth)

### HTTP request headers

- **Content-Type**: Not defined
- **Accept**: `application/json`


### HTTP response details
| Status code | Description | Response headers |
|-------------|-------------|------------------|
| **200** | Response on success. |  -  |
| **0** | Response on failure. |  -  |

[[Back to top]](#) [[Back to API list]](../README.md#api-endpoints) [[Back to Model list]](../README.md#models) [[Back to README]](../README.md)


## getRouteId

> RouteIdentifier getRouteId(listOfLocations, profile)



Returns a routeId representing a route with the specified list of locations. The route is calculated using the same routing algorithm as the calculateMatrix and startMatrixCalculation operations.\\ The returned **routeId** can be then used in combination with the Routing API to retrieve further details about the route, e.g polyline.

### Example

```ts
import {
  Configuration,
  MatricesApi,
} from '';
import type { GetRouteIdRequest } from '';

async function example() {
  console.log("🚀 Testing  SDK...");
  const config = new Configuration({ 
    // To configure API key authorization: apiKeyAuth
    apiKey: "YOUR API KEY",
  });
  const api = new MatricesApi(config);

  const body = {
    // ListOfLocations
    listOfLocations: ...,
    // string | A profile defines a vehicle by a set of attributes, matching typical transport situations. It must be the name of one of the [predefined profiles](./concepts/profiles-and-countries) such as _EUR_TRAILER_TRUCK_. (optional)
    profile: profile_example,
  } satisfies GetRouteIdRequest;

  try {
    const data = await api.getRouteId(body);
    console.log(data);
  } catch (error) {
    console.error(error);
  }
}

// Run the test
example().catch(console.error);
```

### Parameters


| Name | Type | Description  | Notes |
|------------- | ------------- | ------------- | -------------|
| **listOfLocations** | [ListOfLocations](ListOfLocations.md) |  | |
| **profile** | `string` | A profile defines a vehicle by a set of attributes, matching typical transport situations. It must be the name of one of the [predefined profiles](./concepts/profiles-and-countries) such as _EUR_TRAILER_TRUCK_. | [Optional] [Defaults to `&#39;EUR_TRAILER_TRUCK&#39;`] |

### Return type

[**RouteIdentifier**](RouteIdentifier.md)

### Authorization

[apiKeyAuth](../README.md#apiKeyAuth)

### HTTP request headers

- **Content-Type**: `application/json`
- **Accept**: `application/json`


### HTTP response details
| Status code | Description | Response headers |
|-------------|-------------|------------------|
| **200** | Response on success. |  -  |
| **0** | Response on failure. |  -  |

[[Back to top]](#) [[Back to API list]](../README.md#api-endpoints) [[Back to Model list]](../README.md#models) [[Back to README]](../README.md)


## getStatus

> StatusResponse getStatus(id, maximumPollingPeriod)



Requests the status of a matrix calculation.

### Example

```ts
import {
  Configuration,
  MatricesApi,
} from '';
import type { GetStatusRequest } from '';

async function example() {
  console.log("🚀 Testing  SDK...");
  const config = new Configuration({ 
    // To configure API key authorization: apiKeyAuth
    apiKey: "YOUR API KEY",
  });
  const api = new MatricesApi(config);

  const body = {
    // string | The ID of a matrix calculation operation.
    id: 38400000-8cf0-11bd-b23e-10b96e4ef00d,
    // number | If the calculation is still running, this operation will be blocked and will not return before this period [ms] expires. If the calculation is completed, it will return immediately.  The default of 0 ms will cause the operation to return immediately in any case. Use a value > 0 to implement long polling to reduce the number of requests. See the [tutorial](https://developer.myptv.com/en/resources/tutorials/general/how-use-asynchronous-requests-ptv-developer-apis) on asynchronous requests for details.  (optional)
    maximumPollingPeriod: 56,
  } satisfies GetStatusRequest;

  try {
    const data = await api.getStatus(body);
    console.log(data);
  } catch (error) {
    console.error(error);
  }
}

// Run the test
example().catch(console.error);
```

### Parameters


| Name | Type | Description  | Notes |
|------------- | ------------- | ------------- | -------------|
| **id** | `string` | The ID of a matrix calculation operation. | [Defaults to `undefined`] |
| **maximumPollingPeriod** | `number` | If the calculation is still running, this operation will be blocked and will not return before this period [ms] expires. If the calculation is completed, it will return immediately.  The default of 0 ms will cause the operation to return immediately in any case. Use a value &gt; 0 to implement long polling to reduce the number of requests. See the [tutorial](https://developer.myptv.com/en/resources/tutorials/general/how-use-asynchronous-requests-ptv-developer-apis) on asynchronous requests for details.  | [Optional] [Defaults to `0`] |

### Return type

[**StatusResponse**](StatusResponse.md)

### Authorization

[apiKeyAuth](../README.md#apiKeyAuth)

### HTTP request headers

- **Content-Type**: Not defined
- **Accept**: `application/json`


### HTTP response details
| Status code | Description | Response headers |
|-------------|-------------|------------------|
| **200** | Response on success. |  -  |
| **0** | Response on failure. |  -  |

[[Back to top]](#) [[Back to API list]](../README.md#api-endpoints) [[Back to Model list]](../README.md#models) [[Back to README]](../README.md)


## startMatrixCalculation

> MatrixIdentifier startMatrixCalculation(locations, profile, results, options)



Creates a matrix asynchronously by calculating distances, travel times and toll costs between given origins and destinations.\\ The request is rejected if the number of relations (number of origins * number of destinations) is greater than 4,000,000 (see also the [FAQ](../../help/faq-help) for details regarding limits).\\ Please note that toll cost and time-dependent calculations significantly increase the operation runtime.\\ Gzip-encoded content is supported in the request body.

### Example

```ts
import {
  Configuration,
  MatricesApi,
} from '';
import type { StartMatrixCalculationRequest } from '';

async function example() {
  console.log("🚀 Testing  SDK...");
  const config = new Configuration({ 
    // To configure API key authorization: apiKeyAuth
    apiKey: "YOUR API KEY",
  });
  const api = new MatricesApi(config);

  const body = {
    // Locations
    locations: ...,
    // string | A profile defines a vehicle by a set of attributes, matching typical transport situations. It must be the name of one of the [predefined profiles](./concepts/profiles-and-countries) such as _EUR_TRAILER_TRUCK_. (optional)
    profile: profile_example,
    // Array<Results> | Comma-separated list that defines which results will be returned.  * `DISTANCES`     Response includes information about the distances between start and destination locations.  * `TRAVEL_TIMES`     Response includes information about the travel times between start and destination locations.  * `TOLL_COSTS`     Response includes information about the toll costs between start and destination locations.     Toll tariffs are evaluated based on the date and time specified in `options[tollTime]` when `options[trafficMode]` is set to _AVERAGE_ or `options[startTime]` when `options[trafficMode]` is set to _CONSTANT_.     If no date and time are provided, tolls are calculated using the tariffs valid at noon on Monday of the current week.     For custom routing profiles, the UTC offset is derived from the profile\'s timezone setting, accounting for daylight saving time.     For predefined profiles, a representative timezone for the profile\'s region is used:     * _EUROPE_ - Central European Time / Central European Summer Time (UTC+01:00/+02:00)     * _AMERICA_ - Central Time (UTC-06:00/-05:00)     * _IMEA_ - Arabia Standard Time (UTC+03:00)     * _AUSTRALIA_ - Australian Eastern Time (UTC+10:00/+11:00)     * _WORLD_ - UTC (+00:00)      **Only available for startMatrixCalculation operation.**  * `DIRECT_DISTANCE_FLAGS`     Response includes flags describing if relations have been estimated by direct distance.  * `VIOLATION_FLAGS`     Response includes flags describing if relations contain violations. (optional)
    results: ["TRAVEL_TIMES"],
    // Options | Matrix Routing-relevant options like the currency for the toll costs. Use array notation like `options[currency]=EUR` to set options. (optional)
    options: ...,
  } satisfies StartMatrixCalculationRequest;

  try {
    const data = await api.startMatrixCalculation(body);
    console.log(data);
  } catch (error) {
    console.error(error);
  }
}

// Run the test
example().catch(console.error);
```

### Parameters


| Name | Type | Description  | Notes |
|------------- | ------------- | ------------- | -------------|
| **locations** | [Locations](Locations.md) |  | |
| **profile** | `string` | A profile defines a vehicle by a set of attributes, matching typical transport situations. It must be the name of one of the [predefined profiles](./concepts/profiles-and-countries) such as _EUR_TRAILER_TRUCK_. | [Optional] [Defaults to `&#39;EUR_TRAILER_TRUCK&#39;`] |
| **results** | `Array<Results>` | Comma-separated list that defines which results will be returned.  * &#x60;DISTANCES&#x60;     Response includes information about the distances between start and destination locations.  * &#x60;TRAVEL_TIMES&#x60;     Response includes information about the travel times between start and destination locations.  * &#x60;TOLL_COSTS&#x60;     Response includes information about the toll costs between start and destination locations.     Toll tariffs are evaluated based on the date and time specified in &#x60;options[tollTime]&#x60; when &#x60;options[trafficMode]&#x60; is set to _AVERAGE_ or &#x60;options[startTime]&#x60; when &#x60;options[trafficMode]&#x60; is set to _CONSTANT_.     If no date and time are provided, tolls are calculated using the tariffs valid at noon on Monday of the current week.     For custom routing profiles, the UTC offset is derived from the profile\&#39;s timezone setting, accounting for daylight saving time.     For predefined profiles, a representative timezone for the profile\&#39;s region is used:     * _EUROPE_ - Central European Time / Central European Summer Time (UTC+01:00/+02:00)     * _AMERICA_ - Central Time (UTC-06:00/-05:00)     * _IMEA_ - Arabia Standard Time (UTC+03:00)     * _AUSTRALIA_ - Australian Eastern Time (UTC+10:00/+11:00)     * _WORLD_ - UTC (+00:00)      **Only available for startMatrixCalculation operation.**  * &#x60;DIRECT_DISTANCE_FLAGS&#x60;     Response includes flags describing if relations have been estimated by direct distance.  * &#x60;VIOLATION_FLAGS&#x60;     Response includes flags describing if relations contain violations. | [Optional] |
| **options** | [](.md) | Matrix Routing-relevant options like the currency for the toll costs. Use array notation like &#x60;options[currency]&#x3D;EUR&#x60; to set options. | [Optional] [Defaults to `undefined`] |

### Return type

[**MatrixIdentifier**](MatrixIdentifier.md)

### Authorization

[apiKeyAuth](../README.md#apiKeyAuth)

### HTTP request headers

- **Content-Type**: `application/json`
- **Accept**: `application/json`


### HTTP response details
| Status code | Description | Response headers |
|-------------|-------------|------------------|
| **202** | Response on success. |  -  |
| **0** | Response on failure. |  -  |

[[Back to top]](#) [[Back to API list]](../README.md#api-endpoints) [[Back to Model list]](../README.md#models) [[Back to README]](../README.md)

