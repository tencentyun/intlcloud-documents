## Example of Importing APIs in the YAML Format
```yaml
openapi: 3.0.0
info:
  description: importMockAPI
  version: "1.0.0"
  title: Mock API
paths:
  /mock:
    get:
      description: Import Mock API Test
      operationId: importMockAPI
      responses:
        '200':
          description: Import Mock API Test
```

## Example of Importing APIs in the JSON Format
```json
{
  "openapi": "3.0.0",
  "info": {
    "description": "importMockAPI",
    "version": "1.0.0",
    "title": "Mock API"
  },
  "paths": {
    "/mock": {
      "get": {
        "description": "Import Mock API Test",
        "operationId": "importMockAPI",
        "responses": {
          "200": {
            "description": "Import Mock API Test"
          }
        }
      }
    }
  }
}
```
