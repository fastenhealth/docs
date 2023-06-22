---
layout: default
title: Query Syntax - FHIR Search API
parent: Dashboard
---

The `where` clause syntax for Fasten Dashboard Widgets is based on the official [FHIR Search API syntax](http://hl7.org/fhir/R4/search.html)
with some modifications.


```json
{
  "q": {
    "select": [
      ...
    ],
    "from": "Observation",
    "where": {
      "code": "http://loinc.org|29463-7,http://loinc.org|3141-9,http://snomed.info/sct|27113001"
    }
  }
}
```


# Introduction
At it's most basic, the FHIR Search API syntax is a search by key-value pairs against a list of predefined Search Parameter 
keys for each FHIR Resource.

Each search parameter has a specific type, and the allowed value must match the type. For example, the `code` search parameter for
the `Observation` resource has a type of `token`, which means the value must be a string in the format `system|code`.

The FHIR Search API syntax is designed to be used in a URL query string, but in our case we're using it within a JSON object.


- [Search Parameters for each FHIR Resource](http://hl7.org/fhir/R4/searchparameter-registry.html)
- [FHIR Search API Syntax](http://hl7.org/fhir/R4/search.html)

# Standard Search Parameters

The following parameters apply to all resources: `content`, `id`, `lastUpdated`, `profile`, `query`, `security`, `source`, `tag`. 

The search parameter `id` refers to the logical id of the resource, and can be used when the search context specifies a resource type:

```
{
    "from": "Patient",
    "where": {
        "id": "123"
    }
}
```

This search finds the patient resource with the given id. Functionally, this is equivalent to a simple read operation:

`GET [base]/Patient/23`


The search parameter `lastUpdated` can be used to select resources based on the last time they were changed:

```jsonc
// GET [base]/Observation?_lastUpdated=gt2010-10-01
{
    "from": "Observation",
    "where": {
        "lastUpdated": "gt2010-10-01"
    }
}
```

# Search Parameter Types

Each search parameter is defined by a type that specifies how the search parameter behaves. These are the defined parameter types:

| Type | Description                                                                                                                                                                                                                                                                                                          |
| --- |----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| number | Search parameter SHALL be a number (a whole number, or a decimal).                                                                                                                                                                                                                                                   |                                                                                                                                                                                                   
| date | Search parameter is on a date/time. The date format is the standard XML format, though other formats may be supported.                                                                                                                                                                                               |                                                                                                                              
| string | Search parameter is a simple string, like a name part. Search is case-insensitive and accent-insensitive. May match just the start of a string. String parameters may contain spaces.                                                                                                                                |                                                                            
| token | Search parameter on a coded element or identifier. May be used to search through the text, display, code and code/codesystem (for codes) and label, system and key (for identifier). Its value is either a string or a pair of namespace and value, separated by a "pipe" character, depending on the modifier used. |
| reference | A reference to another resource (Reference or canonical).                                                                                                                                                                                                                                                            |                                                                                                                                                                                                                                                           
| quantity | A search parameter that searches on a quantity.                                                                                                                                                                                                                                                                      |                                                                                                                                                                                                                                                         
| uri | A search parameter that searches on a URI (RFC 3986).                                                                                                                                                                                                                                                                |                                                                                                                                                                                                                                                   

The search parameters can also append "modifiers" that control their behavior. The kinds of modifiers that available is dependent on the type of parameter being modified. 

## Number
