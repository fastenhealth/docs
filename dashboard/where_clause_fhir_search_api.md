---
layout: default
title: Where Clause - FHIR Search API
parent: Query Syntax
grand_parent: Dashboard
nav_order: 3
---

# Query Syntax - FHIR Search API

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


## Introduction
At it's most basic, the FHIR Search API syntax is a search by key-value pairs against a list of predefined Search Parameter 
keys for each FHIR Resource.

Each search parameter has a specific type, and the allowed value must match the type. For example, the `code` search parameter for
the `Observation` resource has a type of `token`, which means the value must be a string in the format `system|code`.

The FHIR Search API syntax is designed to be used in a URL query string, but in our case we're using it within a JSON object.


- [Search Parameters for each FHIR Resource](http://hl7.org/fhir/R4/searchparameter-registry.html)
- [FHIR Search API Syntax](http://hl7.org/fhir/R4/search.html)

## Standard Search Parameters

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

## Search Parameter Types

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


## Prefixes

For the ordered parameter types of [number](#number), [date](#date), and [quantity](#quantity), a prefix to the parameter value may be used to control the nature of the matching. 

| Prefix | Description                                                                                      |
| --- |--------------------------------------------------------------------------------------------------|
| `eq` | the value for the parameter in the resource is equal to the provided value                       |
| `ne` | the value for the parameter in the resource is not equal to the provided value                   |
| `gt` | the value for the parameter in the resource is greater than the provided value                   |
| `lt` | the value for the parameter in the resource is less than the provided value                      |
| `ge` | the value for the parameter in the resource is greater or equal to the provided value            |
| `le` | the value for the parameter in the resource is less or equal to the provided value               |
| `sa` | the value for the parameter in the resource starts after the provided value                      |
| `eb` | the value for the parameter in the resource ends before the provided value                       |
| ~~`ap`~~ | ~~the value for the parameter in the resource is approximately the same to the provided value.~~ | 


If no prefix is present, the prefix `eq` is assumed. 


## `number`
<a name="number"></a>
Searching on a simple numerical value in a resource. Examples:

| Search                  | Description |
|-------------------------| --- |
| `"[parameter]": "100"`    | Values that equal 100, to 3 significant figures precision, so this is actually searching for values in the range \[99.5 ... 100.5)
| `"[parameter]": "100.00"` | Values that equal 100, to 5 significant figures precision, so this is actually searching for values in the range \[99.995 ... 100.005)
| `"[parameter]": "1e2"`    | Values that equal 100, to 1 significant figures precision, so this is actually searching for values in the range \[95 ... 105)
| `"[parameter]": "lt100"`  | Values that are less than exactly 100
| `"[parameter]": "le100"`  | Values that are less or equal to exactly 100
| `"[parameter]": "gt100"`  | Values that are greater than exactly 100
| `"[parameter]": "ge100"`  | Values that are greater or equal to exactly 100
| `"[parameter]": "ne100"`  | Values that are not equal to 100 (actually, in the range 99.5 to 100.5)

Notes about searching on Numbers:

*   When a comparison prefix in the set `lgt, lt, ge, le, sa & eb` is provided, the implicit precision of the number is ignored, and they are treated as if they have arbitrarily high precision
*   The way search parameters operate in resources is not the same as whether two numbers are equal to each other in a mathematical sense

Here are some example searches:

**Search**

| Query | Description |
| -- | --- |
| `{"from": "RiskAssessment","where": {"probability": "gt0.8"}}` | Search for all the Risk Assessments with probability great than 0.8 (could also be `probability=gt8e-1` using exponential form)
| `{"from": "ImmunizationRecommendation","where": {"doseNumber": "gt2"}}` | Search for any immunization recommendation recommending a second dose

## `date`
<a name="date"></a>

A date parameter searches on a date/time or period. As is usual for date/time related functionality, while the concepts are 
relatively straight-forward, there are a number of subtleties involved in ensuring consistent behavior.

The date parameter format is `yyyy-mm-ddThh:mm:ss[Z|(+|-)hh:mm]` (the standard RFC3339 format).

Technically, this is any of the [date](datatypes.html#date), [dateTime](datatypes.html#dateTime), and [instant](datatypes.html#instant) 
data types; e.g. Any degree of precision can be provided, but it SHALL be populated from the left (e.g. can't specify a 
month without a year), except that the minutes SHALL be present if an hour is present, and you SHOULD provide a time 
zone if the time part is present. Note: Time can consist of hours and minutes with no seconds, unlike the XML Schema 
dateTime type. Some user agents may escape the `:` characters in the URL, and servers SHALL handle this correctly.

Implicitly, a missing lower boundary is "less than" any actual date. A missing upper boundary is "greater than" any actual date. The use of the prefixes:

| Query | Description                                                                                                                                             |
| --- |---------------------------------------------------------------------------------------------------------------------------------------------------------| 
| `"[parameter]": "eq2013-01-14"` | <ul><li>2013-01-14T00:00 matches (obviously)</li><li>2013-01-14T10:00 matches</li><li>2013-01-15T00:00 does not match - it's not in the range</li></ul> |
| `"[parameter]": "ne2013-01-14"` | <ul><li>2013-01-15T00:00 matches - it's not in the range</li><li>2013-01-14T00:00 does not match - it's in the range</li><li>2013-01-14T10:00 does not match - it's in the range</li></ul> |
| `"[parameter]": "lt2013-01-14T10:00"` | <ul><li>2013-01-14 matches, because it includes the part of 14-Jan 2013 before 10am</li></ul>
| `"[parameter]": "gt2013-01-14T10:00"` | <ul><li>2013-01-14 matches, because it includes the part of 14-Jan 2013 after 10am</li></ul>
| `"[parameter]": "ge2013-03-14"` | <ul><li>"from 21-Jan 2013 onwards" is included because that period may include times after 14-Mar 2013</li></ul>
| `"[parameter]": "le2013-03-14"` | <ul><li>"from 21-Jan 2013 onwards" is included because that period may include times before 14-Mar 2013</li></ul>
| `"[parameter]": "sa2013-03-14"` | <ul><li>"from 15-Mar 2013 onwards" is included because that period starts after 14-Mar 2013</li><li>"from 21-Jan 2013 onwards" is not included because that period starts before 14-Mar 2013</li><li>"before and including 21-Jan 2013" is not included because that period starts (and ends) before 14-Mar 2013</li></ul>
| `"[parameter]": "eb2013-03-14"` | <ul><li>"from 15-Mar 2013 onwards" is not included because that period starts after 14-Mar 2013</li><li>"from 21-Jan 2013 onwards" is not included because that period starts before 14-Mar 2013, but does not end before it</li><li>"before and including 21-Jan 2013" is included because that period ends before 14-Mar 2013</li></ul>
| `"[parameter]": "ap2013-03-14"` | <ul><li>14-Mar 2013 is included - as it exactly matches</li><li>21-Jan 2013 is not included because that is near 14-Mar 2013</li><li>15-Jun 2015 is not included - as it is not near 14-Mar 2013. Note that the exact value here is at the discretion of the system</li></ul>


To search for all the procedures in a patient compartment that occurred over a 2-year period:

```json
{
  "from": "Procedure",
    "where": {
        "date": ["ge2010-01-01", "le2011-12-31"]
    }
}
```
![](assets/images/dragon.png "Here Be Dragons!")

Fasten doesn't yet take into account the timezone of the record or the client. 
## `string`
<a name="string"></a>

For a simple string search, a string parameter serves as the input for a search against sequences of characters. 
This search is insensitive to casing and included combining characters, like accents or other diacritical marks. 
By default, a field matches a string query if the value of the field equals or starts with the supplied parameter value, 
after both have been normalized by case and combining characters. Therefore, the default string search only operates on 
the base characters of the string parameter. The `:contains` modifier returns results that include the supplied parameter 
value anywhere within the field being searched. The `:exact` modifier returns results that match the entire supplied 
parameter, including casing and accents.

Examples:

```json
{
    "from": "Patient",
    "where": {
        "given": "eve"
    }
}
```

Any patients with a name containing a given part with "eve" at the start of the name. This would include patients with the given name "Eve", "Evelyn".

```json
{
    "from": "Patient",
    "where": {
        "given:contains": "eve"
    }
}
```

Any patients with a name with a given part containing "eve" at any position. This would include patients with the given name "Eve", "Evelyn", and also "Severine".

```json
{
    "from": "Patient",
    "where": {
        "given:exact": "Eve"
    }
}
```
Any patients with a name with a given part that is exactly "Eve". Note: This would not include patients with the given name "eve" or "EVE".


