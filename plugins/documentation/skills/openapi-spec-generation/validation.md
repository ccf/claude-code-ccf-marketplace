# OpenAPI Validation Patterns

## Spectral Configuration

Create `.spectral.yaml` for custom rules:

```yaml
extends: ['spectral:oas']

rules:
  # Require operationId
  operation-operationId: error

  # Require descriptions
  operation-description: warn
  info-description: error

  # Naming conventions
  paths-kebab-case:
    given: '$.paths[*]~'
    severity: error
    then:
      function: pattern
      functionOptions:
        match: '^(/[a-z0-9-]+)+$'

  # Require examples
  schema-examples:
    given: '$.components.schemas[*]'
    severity: warn
    then:
      field: example
      function: truthy
```

## Validation Commands

```bash
# Lint with Spectral
npx @stoplight/spectral-cli lint openapi.yaml

# Validate with openapi-generator
npx openapi-generator-cli validate -i openapi.yaml

# Bundle multi-file specs
npx @redocly/cli bundle openapi.yaml -o bundled.yaml

# Preview documentation
npx @redocly/cli preview-docs openapi.yaml
```

## CI/CD Integration

### GitHub Actions

```yaml
name: OpenAPI Validation
on: [push, pull_request]

jobs:
  validate:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4

      - name: Lint OpenAPI spec
        uses: stoplightio/spectral-action@v0.8.10
        with:
          file_glob: 'openapi.yaml'

      - name: Validate spec
        run: |
          npx openapi-generator-cli validate -i openapi.yaml
```

## Common Validation Errors

| Error                   | Cause                      | Fix                               |
| ----------------------- | -------------------------- | --------------------------------- |
| `$ref not found`        | Invalid reference path     | Check component names match       |
| `Missing operationId`   | No unique ID for operation | Add `operationId: uniqueName`     |
| `Invalid schema`        | Malformed JSON Schema      | Validate schema types and formats |
| `Duplicate operationId` | Same ID used twice         | Ensure each operationId is unique |

## Contract Testing

```javascript
// Jest + supertest example
const request = require('supertest')
const OpenAPIValidator = require('express-openapi-validator')

describe('API Contract Tests', () => {
  beforeAll(async () => {
    await OpenAPIValidator.middleware({
      apiSpec: './openapi.yaml',
      validateRequests: true,
      validateResponses: true,
    })
  })

  it('GET /users returns valid response', async () => {
    const response = await request(app).get('/users').expect(200)

    // Response automatically validated against spec
    expect(response.body.data).toBeDefined()
  })
})
```
