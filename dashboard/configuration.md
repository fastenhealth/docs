---
layout: default
title: Configuration
parent: Dashboard
nav_order: 2
---

Dashboards are defined in a simple JSON syntax.

```json
{
  "id": "example_dashboard",
  "schema_version": "1.0",
  "title": "Example Dashboard",
  "description": "An example dashboard to show-off the power of Fasten widgets",
  "widgets": [
    {
      "title_text": "Diabetes Tracking",
      "description_text": "Track key metrics for your chronic disease (eg. Diabetes). The data within this widget is not reflective of your health record, and is only present for demonstrational purposes.",
      "x": 0,
      "y": 0,
      "width": 8,
      "height": 5,
      "item_type": "complex-line-widget"
    }
  ]
}
```

- `id` - A unique identifier for the dashboard. This is used to store the dashboard in the database.
- `schema_version` - The version of the schema used to define the dashboard. This is used to ensure that the dashboard is compatible with the current version of Fasten.
- `title` - The title of the dashboard. This is displayed in the top-left corner of the dashboard.
- `description` - A description of the dashboard. This is displayed at the top of the dashboard.
- `widgets` - A list of widgets to display on the dashboard. See the [Widgets](#widgets) section for more info.

Note, the dashboard is made up of a grid, with a max width of 12.
Widgets are placed on this grid, and their position is defined by the `x` and `y` properties (as discussed below). The `width` and `height` properties define the size of the widget in cells.

# Widgets
<a name="widgets"></a>

Widgets are the building blocks of a dashboard. They are the individual components that are displayed on the dashboard.
There are a number of widgets available, primarily differentiated by the type of graph they display.
Most widgets also allow the user to specify a query to run against their medical records, to customize the data displayed in the graph.

There are also a number of pre-defined widgets that use pre-defined queries to display common data. (Vital Signs, etc)

## Widget Properties

All widgets have the same basic properties:

```json
{
  "title_text": "Weight",
  "description_text": "",
  "x": 8,
  "y": 0,
  "width": 2,
  "height": 2,
  "item_type": "simple-line-chart-widget",
  "queries": [{
    "q": {
      "select": [
        "valueQuantity.value as data",
        "(effectiveDateTime | issued).first() as label"
      ],
      "from": "Observation",
      "where": {
       "code": "http://loinc.org|29463-7,http://loinc.org|3141-9,http://snomed.info/sct|27113001"
      }
    },
    "dataset_options": {}
  }],
  "parsing": {
    "xAxisKey": "label",
    "yAxisKey": "data"
  }
}
```

- `title_text` - The title of the widget. This is displayed at the top of the widget.
- `description_text` [OPTIONAL] - A description of the widget. May be displayed within the widget.
- `x` - The x-coordinate of the widget on the dashboard.
- `y` - The y-coordinate of the widget on the dashboard.
- `width` - The width of the widget in cells.
- `height` - The height of the widget in cells.
- `item_type` - The type of widget. See [Widget Types](#widget-types) for more info.
- `queries` [OPTIONAL] - A list of queries to run against the user's medical records. See [Query Syntax](#query_syntax) for more info.
- `parsing` [OPTIONAL] - A set of rules to parse the results of the query. See [Query Syntax](#query_syntax) for more info.
- `aggregations` [OPTIONAL] - A clause which can be used to group or aggregate the results

## Widget Types
<a name="widget-types"></a>
> If there's a chart/widget type from [ChartJS](https://www.chartjs.org/) that you'd like to use, but is missing in Fasten, please open a [Github Issue](https://github.com/fastenhealth/fasten-onprem/issues), we'd be happy to add it for you. 

### Simple Line Widget

- set the `item_type` to `simple-line-chart-widget`

### Complex Line Widget

- set the `item_type` to `complex-line-chart-widget`

### Donut Chart Widget

- set the `item_type` to `donut-chart-widget`

### Dual Gauges Widget

- set the `item_type` to `dual-gauges-widget`

### Grouped Bar Chart Widget

- set the `item_type` to `grouped-bar-chart-widget`

### Table Widget

- set the `item_type` to `table-widget`


## Query Syntax
<a name="query_syntax"></a>

Queries are used to retrieve data from the user's medical records. They are defined using a simple JSON syntax.
The JSON syntax is similar to SQL, but is designed to query deeply nested FHIR resources. 

```json
{
  "q": {
    "select": [
      "valueQuantity.value as data",
      "(effectiveDateTime | issued).first() as label"
    ],
    "from": "Observation",
    "where": {
     "code": "http://loinc.org|29463-7,http://loinc.org|3141-9,http://snomed.info/sct|27113001"
    }
  },
  "dataset_options": {
    "label": "string",
    "borderWidth": 0,
    "borderColor": "string",
    "fill": false,
    "backgroundColor": "string",
  }
}
```
The query is broken up into the following elements, each of which are handled by a slightly different query syntax:


- `q.from` [OPTIONAL] - The FHIR resource type to query. This will limit the search to a specific table in the database.
- `q.select` - An array of FHIRPath statements. Each statement will be evaluated against the FHIR resource, extracting potentially deeply nested data and making it available for graphing. See [FHIRPath Syntax](#fhirpath) for more info.
- `q.where` - The conditions to apply when querying the database. Uses the FHIR Search API syntax to determine which resources to return (for subsequent FHIRPath processing in the Select clause) [FHIR Search API Syntax](#fhir_search_api) for more info.
- `dataset_options` [OPTIONAL] - The display/visualization options to apply to the dataset when generating the widget chart. See [ChartJS DataSet Options Syntax](#dataset_options_syntax) for more info.
