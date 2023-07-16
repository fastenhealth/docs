---
layout: default
title: Select Clause
parent: Query Syntax
grand_parent: Dashboard
nav_order: 1
---

# Select Clause - FHIRPath

The `select` clause syntax for Fasten Dashboard Widgets is based on the official [FhirPath query syntax](http://hl7.org/fhirpath/)
with some simplifications.


```json
{
  "q": {
    "select": [
      "valueQuantity.value as data",  
      "(effectiveDateTime | issued).first() as label"
    ],
    "from": "Observation",
    "where": {
      ...
    }
  }
}
```


The `select` clause does what you expect it to do. It is a projection from the original FHIR structure to the defined field list in the clause.

## Field list

In the `select` statement you define a FHIRPath query list, and a query can have several forms:

### Simple field name

You can just define a field name just like you would do in SQL.

```json
{
  "q": {
    "select": [
      "name",  
    ],
    "from": "Patient",
    "where": {
      ...
    }
  }
}
```

 Because `'name'` is a FHIRPath expression, you must remember that this does not produce a single value. That means that if there is more than one name in the resource, they will all go to the output.

Name is also an object in itself, because it contains sub fields. This query will therefore also produce a set of name-objects in the output.

### All fields

You can use the `*` query in the select statement to return the FHIR resource as-is:

```json
{
  "q": {
    "select": [
      "*",  
    ],
    "from": "Patient",
    "where": {
      ...
    }
  }
}
```

### Field Aliases

You can explicitly set an alias/name for a query using the `as` query format:

```json
{
  "q": {
    "select": [
      "valueQuantity.value as data",  
      "(effectiveDateTime | issued).first() as label"
    ],
    "from": "Observation",
    "where": {
      ...
    }
  }
}
```
