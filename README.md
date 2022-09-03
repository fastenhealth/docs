# docs

# Features
- Integrate with popular health portals
- Track events (calendar)?
- Upload photo records
- Authentication required
- Encryption at rest
- Integration with external apis 
	- (Apple Health?) 
	- [https://www.researchandcare.org/carekit/](https://www.researchandcare.org/carekit/)
	- smart scales
- Integration with DNA suites
- Historical data from lab results (bloodwork over time)
- Forward emails
- Features:   [https://github.com/carekit-apple/CareKit/tree/master/OCKSample](https://github.com/carekit-apple/CareKit/tree/master/OCKSample)
- [https://awesomeopensource.com/project/carekit-apple/CareKit](https://awesomeopensource.com/project/carekit-apple/CareKit)
- [https://docs.smarthealthit.org/](https://docs.smarthealthit.org/)
- Vaccine records
- Family history


# FHIR

## Authentication/OAuth
- https://build.fhir.org/ig/HL7/smart-app-launch/scopes-and-launch-context.html
- [https://usefulangle.com/post/4/javascript-communication-parent-child-window](https://usefulangle.com/post/4/javascript-communication-parent-child-window)
- 

## Schemas
- [https://schema.org/MedicalEntity](https://schema.org/MedicalEntity)
- [https://www.hl7.org/fhir/overview.html](https://www.hl7.org/fhir/overview.html)
- [https://www.hl7.org/fhir/patient-operation-everything.html](https://www.hl7.org/fhir/patient-operation-everything.html)
- [https://reference.humanapi.co/reference/allergies](https://reference.humanapi.co/reference/allergies)
- [https://fhir.epic.com/Documentation?docId=patientfacingfhirapps](https://fhir.epic.com/Documentation?docId=patientfacingfhirapps)
- [https://docs.microsoft.com/en-us/azure/healthcare-apis/fhir/patient-everything](https://docs.microsoft.com/en-us/azure/healthcare-apis/fhir/patient-everything)
- [https://cloud.google.com/healthcare-api/docs/how-tos/fhir-bundles](https://cloud.google.com/healthcare-api/docs/how-tos/fhir-bundles)
- [https://www.hl7.org/fhir/definitions.json.zip](https://www.hl7.org/fhir/definitions.json.zip)
- 

## Example Datasets
- [https://synthetichealth.github.io/synthea/](https://synthetichealth.github.io/synthea/)
- [http://docs.smarthealthit.org/dstu2-examples/](http://docs.smarthealthit.org/dstu2-examples/)
- [https://github.com/hapifhir/fhir-tutorial/blob/master/Transactions/lesson.md](https://github.com/hapifhir/fhir-tutorial/blob/master/Transactions/lesson.md)

# Architecture

## Golang
- Workers - https://github.com/gocraft/work
- Role based authentication - [https://github.com/Permify/permify-gorm](https://github.com/Permify/permify-gorm)

## Database
- Sqlite
- BerkerleyDB
- LevelDB / RocksDB are more modern, maintained, better for SSD workload
