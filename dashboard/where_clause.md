---
layout: default
title: Where Clause
parent: Query Syntax
grand_parent: Dashboard
nav_order: 3
---

# Where Clause - FHIR Search API

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

```json
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


## `number` Search Parameter Type
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

## `date` Search Parameter Type
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

## `string` Search Parameter Type
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



## `uri` Search Parameter Type
<a name="uri"></a>

The uri parameter refers to an element that contains a URI ([RFC 3986](https://tools.ietf.org/html/rfc3986) ). By default, 
matches are precise (e.g. case, accent, and escape) sensitive, and the entire URI must match. The modifier `:above` or 
`:below` can be used to indicate that partial matching is used. For example:

```json
{
    "from": "ValueSet",
    "where": {
        "url": "http://acme.org/fhir/ValueSet/123"
    }
}
```
```json
{
    "from": "ValueSet",
    "where": {
        "url:below": "http://acme.org/fhir/"
    }
}
```
```json
{
    "from": "ValueSet",
    "where": {
        "url:above": "http://acme.org/fhir/ValueSet/123/_history/5"
    }
}
```

```json
{
    "from": "ValueSet",
    "where": {
      "url": "urn:oid:1.2.3.4.5"
    }
}
```

*   The first line is a request to find any value set with the exact url "http://acme.org/fhir/ValueSet/123"
*   The second line performs a search that will return any value sets that have a URL that starts with "http://acme.org/fhir/"
*   The third line shows the converse - search for any value set above a given specific URL. This will match on any value set with the specified URL, but also on http://acme.org/ValueSet/123. Note that there are not many use cases where :above is useful as compared to the `:below` search
*   The fourth line shows an example of searching by an OID. Note that the :above and :below modifiers only apply to URLs, and not URNS such as OIDs

The search type `uri` is used with elements of type [uri](#uri). The type [reference](#reference) is used for the types Reference and
[canonical](datatypes.html#canonical). Note that for `uri` parameters that refer to the [Canonical URLs](references.html#canonical) of 
the conformance and knowledge resources (e.g. [StructureDefinition](structuredefinition.html), [ValueSet](valueset.html), 
[PlanDefinition](plandefinition.html) etc), servers SHOULD support searching by canonical references, and 
SHOULD support automatically detecting a `|[version]` portion as part of the search parameter, and interpreting that 
portion as a search on the version.

## `token` Search Parameter Type
<a name="token"></a>

A token type is a parameter that provides a close to exact match search on a string of characters, potentially scoped by 
a URI. It is mostly used against a code or identifier data type where the value may have a URI that scopes its meaning, 
where the search is performed against the pair from a Coding or an Identifier. Tokens are also used against other fields 
where exact matches are required - uris, booleans, and [ContactPoints](datatypes.html#ContactPoint). In these cases, the 
URI portion is not used.

For tokens, matches are literal (e.g. not based on [subsumption](codesystem.html#subsumption) or other code system features). 
Match is case sensitive unless the underlying semantics for the context indicate that the token should be interpreted 
case-insensitively (see, e.g. [CodeSystem.caseSensitive](codesystem-definitions.html#CodeSystem.caseSensitive)). Note 
that matches on `_id` are always case sensitive. If the underlying data type is `[string](datatypes.html#string)` then 
the search is not case sensitive.

**Note**: There are many challenging issues around case sensitivity and token searches. Some code systems are case sensitive
(e.g. UCUM) while others are known not to be. For many code systems, it's ambiguous. Other kinds of values are also ambiguous. 
When in doubt, servers SHOULD treat tokens in a case-insensitive manner, on the grounds that including undesired data has 
less safety implications than excluding desired behavior. Clients SHOULD always use the correct case when possible, and 
allow for the server to perform case-insensitive matching.

To use subsumption-based logic, use the modifiers below, or list all the codes in the hierarchy. The syntax for the value is one of the following:

*   **`[parameter]=[code]`**: the value of `[code]` matches a Coding.code or Identifier.value irrespective of the value of the system property
*   **`[parameter]=[system]|[code]`**: the value of `[code]` matches a Coding.code or Identifier.value, and the value of `[system]` matches the system property of the Identifier or Coding
*   **`[parameter]=|[code]`**: the value of `[code]` matches a Coding.code or Identifier.value, and the Coding/Identifier has no system property
*   **`[parameter]=[system]|`**: any element where the value of `[system]` matches the system property of the Identifier or Coding

Notes:

*   The namespace URI and code both must be [escaped](#escaping) correctly. If a system is not applicable (e.g. an element of type [uri](datatypes.html#uri), then just the form \[parameter\]=\[code\] is used.
*   For token parameters on elements of type [ContactPoint](datatypes.html#ContactPoint), [uri](datatypes.html#uri), or [boolean](datatypes.html#boolean), the presence of the pipe symbol SHALL NOT be used - only the `[parameter]=[code]` form is allowed



**Modifiers:**

| **Modifier**   | **Use**                                                                                                                                                                                                                                                                                                                                                                                                                                |
|----------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| ~~`:text`~~    | ~~The search parameter is processed as a string that searches text associated with the code/value - either _CodeableConcept.text_, _Coding.display_, or _Identifier.type.text_. In this case, the search functions as a [normal string search](#string)~~                                                                                                                                                                              
| `:not`         | Reverse the code matching described in the paragraph above: return all resources that do not have a matching item. Note that this includes resources that have no value for the parameter - e.g. ?gender:not=male includes all patients that do not have gender = male, including patients that do not have a gender at all                                                                                                            
| `:above`       | The search parameter is a concept with the form `[system]                                                                                                                                                                                                                                                                                                                                                                              |[code]`, and the search parameter tests whether the coding in a resource [subsumes](codesystem.html#subsumption) the specified search code. For example, the search concept has an is-a relationship with the coding in the resource, and this includes the coding itself.
| `:below`       | the search parameter is a concept with the form `[system]                                                                                                                                                                                                                                                                                                                                                                              |[code]`, and the search parameter tests whether the coding in a resource is subsumed by the specified search code. For example, the coding in the resource has an is-a relationship with the search concept, and this includes the coding itself.
| `:in`          | The search parameter is a URI (relative or absolute) that identifies a value set, and the search parameter tests whether the coding is in the specified [value set](valueset.html). The reference may be literal (to an address where the value set can be found) or logical (a reference to ValueSet.url). If the server can treat the reference as a literal URL, it does, else it tries to match known logical ValueSet.url values. 
| ~~`:not-in`~~  | ~~The search parameter is a URI (relative or absolute) that identifies a value set, and the search parameter tests whether the coding is not in the specified value set.~~                                                                                                                                                                                                                                                               
| ~~`:of-type`~~ | ~~The search parameter has the format system~~                                                                                                                                                                                                                                                                                                                                                                                         |code|value, where the system and code refer to a `Identifier.type.coding.system` and `.code`, and match if any of the type codes match. All 3 parts must be present


Example searches:

```json
{
    "from": "Patient",
    "where": {
        "identifier": "http://acme.org/patient|2345"
    }
}
```
Search for all the patients with an identifier with key = "2345" in the system "http://acme.org/patient"

```json
{
  "from": "Patient",
  "where": {
    "gener": "male"
  }
}

```
Search for any patient with a gender that has the code "male"

```json
{
    "from": "Patient",
    "where": {
      "gender:not": "male"
    }
}
```
Search for any patient with a gender that does not have the code "male". Note that for `:not`, the search does not return any resources that have a gen

```json
{
    "from": "Composition",
    "where": {
      "section": "48765-2"
    }
}

```
Search for any Composition that contains an Allergies and adverse reaction section

```json
{
    "from": "Composition",
    "where": {
      "section:not": "48765-2"
    }
}
```
Search for any Composition that does not contain an Allergies and adverse reaction section. Note that this search does not return "any document that has a section that is not an Allergies and adverse reaction section" (e.g. in the presence of multiple possible matches, the _negation_ applies to the set, not each individual entry)

```json
{
    "from": "Patient",
    "where": {
      "active": true
    }
}
```
Search for any patients that are active

```json
{
    "from": "Condition",
    "where": {
      "code": "http://acme.org/conditions/codes|ha125"
    }
}
```
Search for any condition with a code "ha125" in the code system "http://acme.org/conditions/codes"

```json
{
    "from": "Condition",
    "where": {
      "code": "ha125"
    }
}
```
Search for any condition with a code "ha125". Note that there is not often any useful overlap in literal symbols between code systems, so the previous example is generally preferred

```json
{
    "from": "Condition",
    "where": {
      "code:text": "headache"
    }
}
```
Search for any Condition with a code that has a text "headache" associated with it (either in the text, or a display)

```json
{
    "from": "Condition",
    "where": {
      "code:in": "http://snomed.info/sct?fhir_vs=isa/126851005"
    }
}
```
Search for any condition in the SNOMED CT value set "http://snomed.info/sct?fhir\_vs=isa/126851005" that includes all descendants of "Neoplasm of liver"

```json
{
    "from": "Condition",
    "where": {
      "code:below": "126851005"
    }
}
```
Search for any condition that is subsumed by the SNOMED CT Code "Neoplasm of liver". Note: This is the same outcome as the previous search

```json
{
    "from": "Condition",
    "where": {
      "code:in": "http://acme.org/fhir/ValueSet/cardiac-conditions"
    }
}
```
Search for any condition that is in the institutions list of cardiac conditions

```json
{
    "from": "Patient",
    "where": {
      "identifier:of-type": "http://terminology.hl7.org/CodeSystem/v2-0203|MR|446053"
    }
}
```
Search for the Medical Record Number 446053 - this is useful where the system id for the MRN is not known


