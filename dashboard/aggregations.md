---
layout: default
title: Aggregations
parent: Query Syntax
grand_parent: Dashboard
nav_order: 4
---


## Order By

```json
{  
	"select": [],  
	"from": "Observation",  
	"where": {},  
	"aggregations":{  
	  "order_by": "code:code"  
	}  
}
```

## Group By


## Count By

```json
{  
	"select": [],  
	"from": "Observation",  
	"where": {},  
	"aggregations":{  
	  "count_by": "code:code"  
	}  
}
```