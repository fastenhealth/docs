---
layout: default
title: Philosophy
parent: Dashboard
nav_order: 1
---

These are the basic principles that were used when designing the Fasten dashboard.

# Widgets


The goal is for Fasten to have a customizable, widget based Dashboard similar to Grafana/Datadog. 
Users can create personalized dashboards tracking the information they care about, by querying their own medical records using a SQL-like syntax. 


# Sharing

Users can "share" their dashboards. A technical user can do the work of creating a dashboard and configuring 
widgets for a specific chronic disease, and share that dashboard (via a Github Gist/etc). 
Other users can then import this dashboard and use it to view their own medical data. 

# Querying

Given the complexities of FHIR resource data, we're unable to use a simple SQL-like syntax to query the data. 
Instead we're forced to use a more complex approach, using parts from the [FHIR Search API](https://www.hl7.org/fhir/search.html) 
[FHIRPath](https://hl7.org/fhir/fhirpath.html) and SQL.



