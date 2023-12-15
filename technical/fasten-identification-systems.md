
# Fully Qualified Resource Identifier

Since Fasten includes resources from multiple EHR platforms, a `{ResourceType}/{ResourceId}` identifier is not guaranteed to be unique (eg. Encounter/1 could exist on multiple systems)

So Fasten uses the following Reference URI to identify the FHIR resources uniquely:

`urn:fastenhealth-id:${source_id}:${source_resource_type}/${source_resource_id}`

- `source_id` is a UUID generated automatically when storing the SourceCredential in the database
- `source_resource_type` is the FHIR Resource Type
- `source_resource_id` is the FHIR Resource Identifier from the source EHR system


#