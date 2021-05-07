# covidcertificate-apidoc
API documentation for the integration of primary systems with the machine to machine API.

Please import the `api-doc.json` file in the https://editor.swagger.io to see the visualization.

## Error list
There is a custom error body for the request if the server side parameter validation fails.
- `{451, "No vaccination data was specified"}`
- `{452, "No person data was specified"}`
- `{453, "Invalid dateOfBirth! Must be younger than 1900-01-01"}`
- `{454, "Invalid vaccine prophylaxis"}`
- `{455, "Invalid medicinal product"}`
- `{456, "Invalid marketing authorization holder"}`
- `{457, "Invalid number of doses"}`
- `{458, "Invalid vaccination date! Date cannot be in the future"}`
- `{459, "Invalid country of vaccination"}`
- `{460, "Invalid given name! Must not exceed 50 chars"}`
- `{461, "Invalid family name! Must not exceed 50 chars"}`
- `{462, "No test data was specified"}`
- `{463, "Invalid member state of test"}`
- `{464, "Invalid type of test"}`
- `{465, "Invalid test name"}`
- `{466, "Invalid test manufacturer"}`
- `{467, "Invalid testing center or facility"}`
- `{468, "Invalid sample or result date time! Sample date must be before current date and before result date"}`
- `{469, "No recovery data specified"}`
- `{470, "Invalid date of first positive test result"}`
- `{471, "Invalid country of test"}`


