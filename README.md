# docs

> From my [Reddit post announcing Fasten](https://www.reddit.com/r/selfhosted/comments/xj9rx7/introducing_fasten_a_selfhosted_personal/)

Like many of you, I've worked for many companies over my career. 
In that time, I've had multiple health, vision and dental insurance providers, and visited many different clinics, hospitals and labs to get procedures & tests done.

Recently I had a semi-serious medical issue, and I realized that my medical history (and the medical history of my family members) is alot more complicated than I realized and distributed across the many healthcare providers I've used over the years. I wanted a single (private) location to store our medical records, and I just couldn't find any software that worked as I'd like:

- self-hosted/offline - this is my medical history, I'm not willing to give it to some random multi-national corporation to data-mine and sell
- It should aggregate my data from multiple healthcare providers (insurance companies, hospital networks, clinics, labs) across multiple industries (vision, dental, medical) -- all in one dashboard
- automatic - it should pull my EMR (electronic medical record) directly from my insurance provider/clinic/hospital network - I dont want to scan/OCR physical documents (unless I have to)
- open source - the code should be available for contributions & auditing

So, I built it

**Fasten is an open-source, self-hosted, personal/family electronic medical record aggregator, designed to integrate with 1000's of insurances/hospitals/clinics**

Here's a couple of screenshots that'll give you an idea of what it looks like:

[Fasten Screenshots](https://imgur.com/a/vfgojBD)

![](./img/screenshots/2.connect.png)



It's pretty basic right now, but it's designed with a easily extensible core around a solid foundation:

- Self-hosted
- Designed for families, not Clinics (unlike OpenEMR and other popular EMR systems)
- Supports the Medical industry's (semi-standard) FHIR protocol 
- Uses OAuth2 (Smart-on-FHIR) authentication (no passwords necessary)
- Uses OAuth's `offline_access` scope (where possible) to automatically pull changes/updates
- Multi-user support for household/family use
- (Future) Dashboards & tracking for diagnostic tests
- (Future) Integration with smart-devices & wearables

---

See [FAQs](./FAQs.md) for common questions (& answers) regarding Fasten

---

**This is where you come in. I need feedback, lots of it.**

I created a Google Form, and I'd appreciate it if you all filled it out and gave me some indication if this is worthwhile and what kind of monetization model we should follow. 

[https://forms.gle/HqxLL23jxRWvZLKY6](https://forms.gle/HqxLL23jxRWvZLKY6)


Thanks!!


---



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

# Regulations
- 21st Century Cures Act’s Interoperability
- Patient Access Final Rule (CMS-9115-F)
- https://www.cms.gov/Regulations-and-Guidance/Guidance/Interoperability/index
- Trusted Health Data Exchange Framework
	- https://ehrintelligence.com/features/hies-eager-to-join-ambitious-onc-health-data-exchange-framework
- https://www.cms.gov/files/document/faqs-interoperability-patient-access-and-cop-event-notifications-may-2021.pdf
- https://www.cms.gov/files/document/cms-9115-f.pdf
- https://confluence.hl7.org/display/DVP/Da+Vinci+Implementer+Support
- https://www.cmspatientaccessrule.com/
- https://data.cms.gov/provider-compliance
- https://confluence.hl7.org/display/DVP/Da+Vinci+Implementer+Support
- https://www.cmscompliancetracker.com/?page_id=89
- 


### Data Sources
- Electronic Health Records (EHR)
- Patient Portals
- Health Systems
- Hospitals & Doctors
- Pharmacies
- Wearable Devices
- Health Insurers
- Laboratories


### Data Elements
- Explanation of benefits
- Genotypes & genetic traits
- Activity
- Sleep
- Meals
- Healthcare claims
- Immunizations (vaccination status)
- Plans of care
- Narratives
- Conditions
- Medications
- Procedures
- Encounters
- Test results
- Demographics
- Social history
- Vitals/observations
- Organizations

### Insurance Types
- Dental
- Vision
- Medical
- Travel
- Prescription
- Telemedicine
- Mental Health
- Gap
- Short Term
- Hearing
- Disability
- Accident
- Long Term Care
-  Income Protection



# FHIR





## Schemas
- [https://schema.org/MedicalEntity](https://schema.org/MedicalEntity)
- [https://www.hl7.org/fhir/overview.html](https://www.hl7.org/fhir/overview.html)
- [https://www.hl7.org/fhir/patient-operation-everything.html](https://www.hl7.org/fhir/patient-operation-everything.html)
- [https://reference.humanapi.co/reference/allergies](https://reference.humanapi.co/reference/allergies)
- [https://fhir.epic.com/Documentation?docId=patientfacingfhirapps](https://fhir.epic.com/Documentation?docId=patientfacingfhirapps)
- [https://docs.microsoft.com/en-us/azure/healthcare-apis/fhir/patient-everything](https://docs.microsoft.com/en-us/azure/healthcare-apis/fhir/patient-everything)
- [https://cloud.google.com/healthcare-api/docs/how-tos/fhir-bundles](https://cloud.google.com/healthcare-api/docs/how-tos/fhir-bundles)
- [https://www.hl7.org/fhir/definitions.json.zip](https://www.hl7.org/fhir/definitions.json.zip)
- https://docs.sero.run/book/build/patient-access
- https://open.epic.com/Interface/FHIR
- http://clinfhir.com/
- https://fhirbase.aidbox.app/schema - basically store the full json resource in a field
- https://docs.aws.amazon.com/healthlake/latest/devguide/supported-resources.html

> About 33% of respondents favored Epic, whereas 18% decided to renovate their contract with Cerner, and only 7% decided to renovate their contract with Athena Health. This research shows that not all hospitals use Epic; many hospitals also opt for their closest competitors- Cerner, Athena Health and Folio3,
 

## Bulk Data
- https://hl7.org/fhir/uv/bulkdata/

Mandatory Elements
- http://hl7.org/fhir/us/core/StructureDefinition-us-core-patient.html


![](img/bluebutton.png)


## Map between versions
- https://github.com/ahdis/fhir-mapping-tutorial
- https://confluence.hl7.org/display/FHIR/Using+the+FHIR+Mapping+Language
- https://github.com/microsoft/fhir-server/blob/main/docs/ConvertDataOperation.md
- https://github.com/microsoft/FHIR-Converter/


