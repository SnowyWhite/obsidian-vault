# Overview

Here are notes about JavaScripts package manager NPM.

## generate-schema
#CLI #JSON


Convert JSON Objects to MySQL, JSON Schema, Mongoose, Google BigQuery, Swagger, and more.
https://github.com/nijikokun/generate-schema

### Installation

```bash
npm i --save generate-schema (-g for the CLI tool)
```

### CLI

```bash
Usage: generate-schema [options ...] [file]

Common Options:
	-h, --help         output usage information
	-V, --version      output the version number
   -q, --quiet        Skip help message in program output

Mode Options:
	-g, --generic      Generic JSON Primitives schema output
	-j, --json-schema  JSON Schema output
   -s, --mysql        MySQL Table Schema output
   -m, --mongoose     Mongoose Schema output
   -b, --big-query    Google BigQuery Schema output
   -c, --clickhouse   Clickhouse Table Schema output
```

### Code

```js
var GenerateSchema = require('generate-schema')
```

#### Example

```js
// Capture Schema Output
var schema = GenerateSchema.json('Product', [
    {
        "id": 2,
        "name": "An ice sculpture",
        "price": 12.50,
        "tags": ["cold", "ice"],
        "dimensions": {
            "length": 7.0,
            "width": 12.0,
            "height": 9.5
        },
        "warehouseLocation": {
            "latitude": -78.75,
            "longitude": 20.4
        }
    },
    {
        "id": 3,
        "name": "A blue mouse",
        "price": 25.50,
        "dimensions": {
            "length": 3.1,
            "width": 1.0,
            "height": 1.0
        },
        "warehouseLocation": {
            "latitude": 54.4,
            "longitude": -32.7
        }
    }
])

// OUTPUT
{
  "$schema": "http://json-schema.org/draft-04/schema#",
  "title": "Product Set",
  "type": "array",
  "items": {
    "type": "object",
    "properties": {
      "id": {
        "type": "number"
      },
      "name": {
        "type": "string"
      },
      "price": {
        "type": "number"
      },
      "tags": {
        "type": "array",
        "items": {
          "type": "string"
        }
      },
      "dimensions": {
        "type": "object",
        "properties": {
          "length": {
            "type": "number"
          },
          "width": {
            "type": "number"
          },
          "height": {
            "type": "number"
          }
        }
      },
      "warehouseLocation": {
        "type": "object",
        "properties": {
          "latitude": {
            "type": "number"
          },
          "longitude": {
            "type": "number"
          }
        }
      }
    },
    "required": [
      "id",
      "name",
      "price",
      "dimensions",
      "warehouseLocation"
    ],
    "title": "Product"
  }
}
```

#### Methods

`g.generic(Object object)` Generates a generic schema from object. Property types are described using primitives.

`g.mysql([String tableName,] Mixed object)` Generates MySQL Table Schema from object.
- tableName is optional, defaults to generic
- object must be of type Object or Array

`g.json([String title,] Mixed object)` Generates JSON Schema from object.
- title is optional
- object must be of type Object or Array

`g.mongoose(Object object)` Generates a Mongoose Schema from object.

`g.bigquery(Object object)` Generates a Google BigQuery schema from object.

`g.clickhouse([String tableName,] Mixed object, String dateField)` Generates ClickHouse Table Schema from object.
- tableName is optional, defaults to generic
- object must be of type Object or Array
- dateField Date field for ENGINE, must be of type Date