---
layout: default
title: From Clause
parent: Query Syntax
grand_parent: Dashboard
nav_order: 2
---

Fasten stores each FHIR Resource type in its own dedicated database table.
As such, only the following values are acceptable for the `from` clause:

- Account
- AdverseEvent
- AllergyIntolerance
- Appointment
- Binary
- CarePlan
- CareTeam
- Claim
- ClaimResponse
- Composition
- Condition
- Consent
- Coverage
- CoverageEligibilityRequest
- CoverageEligibilityResponse
- Device
- DeviceRequest
- DiagnosticReport
- DocumentManifest
- DocumentReference
- Encounter
- Endpoint
- EnrollmentRequest
- EnrollmentResponse
- ExplanationOfBenefit
- FamilyMemberHistory
- Goal
- ImagingStudy
- Immunization
- InsurancePlan
- Location
- Media
- Medication
- MedicationAdministration
- MedicationDispense
- MedicationRequest
- MedicationStatement
- NutritionOrder
- Observation
- Organization
- OrganizationAffiliation
- Patient
- Person
- Practitioner
- PractitionerRole
- Procedure
- Provenance
- Questionnaire
- QuestionnaireResponse
- RelatedPerson
- Schedule
- ServiceRequest
- Slot
- Specimen
- VisionPrescription

As additional FHIR Resource types are added to the [USCDI](https://www.healthit.gov/isa/united-states-core-data-interoperability-uscdi) specification, or become commonly available by EHR systems, Fasten will support them as well. 
