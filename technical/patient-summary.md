---
title: Patient Summary (IPS)
parent: Technical
---

Fasten Health has the ability to generate a [International Patient Summary (IPS)](https://build.fhir.org/ig/HL7/fhir-ips/index.html) compliant summary. 

We use the following algorithm to determine which FHIR resources to include/exclude from the summary. 

> Note: this algorithm is still a work-in-progress. It is based on the work by [John D'Amore](https://github.com/jddamore) - see: [fhir-ips-serve](https://github.com/jddamore/fhir-ips-server/blob/main/docs/Summary_Creation_Steps.md)



### Data Pipeline

The steps for creating an IPS follow a set of data staging pipeline steps. These are summarized below from code available in the PatientSummary.java class: 

1.	Get all resources related to the patient specified
2.  Initialize `Bundle` and `Composition` 
3.	Assign resources by `ResourceType`, `category` or `code` to 14 IPS sections (see Filtering Logic for more information) 
3.	Evaluate if required resources are missing for required sections. If no resources found, create pseudo resource. 
  a. Allergies List
  b. Problem List
  c. Medication List 
4.	Filter out resources (see Filtering Logic for more information)
5.	Bundle pruning: removal of resources which have been filtered out in pipeline (See Narrative Generation) 
6.	Generate narrative for Composition.section

### Summary Filtering

To create a summary, a set of rules are applied to filter all Patient data down to the relevant content by section for a summary. These rules should be considered preliminary and subject to future revision. 

**Filtering Logic (Preliminary)**
- Allergies (AllergyIntolerance)
  - Don’t want clinicalStatus inactive|resolved 
  - Don’t want verificationStatus entered-in-error
- Problems (Condition)
  - Don’t want clinicalStatus inactive|resolved 
  - Don’t want verificationStatus entered-in-error
- Medications (MedicationStatement and MedicationRequest)
  - MedicationStatement
    - Only status is active|intended|unknown|on-hold
    - For future consideration. Maybe some statuses are filtered out if the period.high is far enough in the past or if status isn’t active… 
  - MedicationRequest
    - Only status is active|unknown|on-hold
-	Results (DiagnosticReport and Observation where category='laboratory'
    - Observation 
      - Exclude all status is preliminary
      - Most recent of each observation.code 
    - DiagnosticReport 
      - No filtering applied
- Vital Signs (Observation where category='vital-signs') 
  - Most recent of each observation.code under category ‘vital-signs’
  - *For consideration, most recent of each* 
    - *Weight*
    - *Height*
    - *BMI*
    - *Head circumference if age <5*
- Social History (Observation where category='social-history')
  - Exclude all status is preliminary
- Pregnancy History (Observation where code is in IPS list)
  - Exclude all status is preliminary
- Immunizations (Immunization)
  - Exclude entered-in-error
- Advance Directive (Consent)
  - Only active status
- Functional Status (ClinicalImpression)
  - Status in-progress | completed
- Medical Devices (DeviceUseStatement)
  - Exclude entered-in-error
- Past History of Illness (Condition)
  - Use dates (Older than five years based on either dateTime or period.high) & clinicalStatus of inactive|remission|resolved 
  - Exclude entered-in-error
- Plan of Care 
  - Include status of active|on-hold|unknown 
- Procedures 
  - Exclude entered-in-error|not-done
  - *For consideration. Some procedures may merit filtering based on dates*

### Narrative Generation

Narrative is required at the `Composition.section.text` within the IPS (see http://build.fhir.org/ig/HL7/fhir-ips/design.html#narrative-and-language-translation). Since individual resources may be loaded into this server with or without `Resource.text`, the server recreates narrative using machine-readable content. 

This narrative creation should be considered preliminary and **DRAFT** and not suitable for production implementation. To edit this formatting, you should edit the following template: hapi-fhir-base/src/main/resources/ca/uhn/fhir/narrative/ips/IPS.html. Each section of the IPS has one or more tables with the following data elements:   

Advance Directives: 
- Scope: Consent.scope.text || Consent.scope.coding[x].display (separated by \<br />)
- Status: Consent.status.code
- Action Controlled: Consent.provision.action[x].{ text || coding[x].display (separated by \<br />)} (concatenate with comma, e.g. x, y, z) 
- Date: Consent.dateTime
 
Allergies And Intolerances: 
- Allergen: AllergyIntolerance.code.text || AllergyIntolerance.code.coding[x].display (separated by \<br />)
- Status: AllergyIntolerance.clinicalStatus.text || AllergyIntolerance.clinicalStatus.coding[x].code (separated by \<br />)
- Category: AllergyIntolerance.category[x] (separated by \<br />)
- Reaction: AllergyIntolerance.reaction.manifestation.description || AllergyIntolerance.reaction.manifestation.text || AllergyIntolerance.reaction.manifestation.coding[x].display (separated by \<br />)
- Severity: AllergyIntolerance.reaction.severity[x].code (separated by \<br />)
- Comments: AllergyIntolerance.note[x].text (separated by \<br />)
- Onset: AllergyIntolerance.onsetDateTime
 
Functional Status: 
- Assessment: ClinicalImpression.code.text ||  ClinicalImpression.code[x].display (separated by \<br />)
- Status: ClinicalImpression.status.code
- Finding:  ClinicalImpression.summary
- Comments: ClinicalImpression.note[x].text (separated by \<br />)
- Date: ClinicalImpression.effectiveDateTime || ClinicalImpression.effectivePeriod.start
 
Immunizations: 
- Immunization: Immunization.vaccineCode.text || Immunization.vaccineCode.coding[x].display (separated by \<br />)
- Status: Immunization.status
- Dose Number: Immunization.protocolApplied[x]{doseNumberPositiveInt || doseNumberString} (concatenate with comma, e.g. x, y, z)            
- Manufacturer: Organization.name
- Lot Number: Immunization.lotNumber
- Comments: Immunization.note[x].text (separated by \<br />)
- Date: Immunization.occurrenceDateTime || Immunization.occurrenceString
 
Medical Devices: 
- Device: Device.type.text || Device.type.coding[x].display (separated by \<br />)
- Status: DeviceUseStatement.status
- Comments: DeviceUseStatement.note[x].text (separated by \<br />)
- Date Recorded: DeviceUseStatement.recordedDateTime
 
Medication Summary: 

TABLE 1: Medication Summary: Medication Requests
- Medication: MedicationRequest.medicationCodeableConcept.text || MedicationRequest.medicationCodeableConcept.coding[x].display (separated by \<br />) || Medication.code.text || Medication.code.coding[x].display (separated by \<br />)
- Status: MedicationRequest.status.display
- Route: MedicationRequest.dosageInstruction[x].{ route.text || route.coding[x].display (separated by \<br />) } (concatenate with comma, e.g. x, y, z) 
- Sig: MedicationRequest.dosageInstruction[x].text (display all sigs separated by \<br />)
- Comments: MedicationRequest.note[x].text (separated by \<br />)
- Authored Date: MedicationRequest.authoredOn
 
TABLE 2: Medication Summary: Medication Statements
- Medication: MedicationStatement.medicationCodeableConcept.text || MedicationStatement.medicationCodeableConcept.coding[x].display (separated by \<br />) || Medication.code.text || Medication.code.coding[x].display (separated by \<br />)
- Status: MedicationStatement.status.display
- Route: MedicationStatement.dosage[x].{ route.text || route.coding[x].display (separated by \<br />) } (concatenate with comma, e.g. x, y, z)
- Sig: MedicationStatement.dosage[x].text (display all sigs separated by \<br />)
- Date: MedicationStatement.effectiveDateTime || MedicationStatement.effectivePeriod.start
 
Plan of Care
- Activity: CarePlan.description
- Intent: CarePlan.intent.code
- Comments: CarePlan.note[x].text (separated by \<br />)
- Planned Start: CarePlan.period.start 
- Planned End: CarePlan.period.end
 
Pregnancy: 
- Code: Observation.code.text || Observation.code.coding[x].display (separated by \<br />)
- Result: Observation.valueQuantity || Observation.valueDateTime || Observation.valueCodeableConcept.text || Observation.valueCodeableConcept.coding[x].display (separated by \<br />) || Observation.valueString
- Comments: Observation.note[x].text (separated by \<br />)
- Date: Observation.effectiveDateTime || Observation.effectivePeriod.start

Problem List: 
- Medical Problems: Condition.code.text || Condition.code.coding[x].display (separated by \<br />)
- Status: Condition.clinicalStatus.text || Condition.clinicalStatus.coding[x].display (separated by \<br />)
- Comments: Condition.note[x].text (separated by \<br />)
- Onset Date: Condition.onsetDateTime || Condition.onsetPeriod.start && “-“ && Condition.onsetPeriod.end || Condition.onsetAge || Condition.onsetRange.low && “-“ && Condition.onsetRange.high || Condition.onsetString

Past History of Illnesses: 
- Medical Problems: Condition.code.text || Condition.code.coding[x].display (separated by \<br />)
- Status: Condition.clinicalStatus.text || Condition.clinicalStatus.coding[x].display (separated by \<br />)
- Comments: Condition.note[x].text (separated by \<br />)
- Onset Date: Condition.onsetDateTime || Condition.onsetPeriod.start && “-“ && Condition.onsetPeriod.end || Condition.onsetAge || Condition.onsetRange.low && “-“ && Condition.onsetRange.high || Condition.onsetString
 
History Of Procedures: 
- Procedure: Procedure.code.text || Procedure.code.coding[x].display (separated by \<br />)
- Comments: Procedure.note[x].text(separated by \<br />)
- Date: Procedure.performedDateTime || Procedure.performedPeriod.start && “-“ && Procedure.performedPeriod.end || Procedure.performedAge || Procedure.performedRange.low && “-“ && Procedure.performedRange.high || Procedure.performedString
 
Diagnostic Results: 

TABLE 1: Diagnostic Results: Observations
- Code: Observation.code.text || Observation.code.coding[x].display (separated by \<br />)
- Result: Observation.valueQuantity || Observation.valueDateTime || Observation.valueCodeableConcept.text || Observation.valueCodeableConcept.coding[x].display (separated by \<br />) || Observation.valueString
- Unit: Observation.valueQuantity.unit
- Interpretation: Observation.interpretation[0].text || Observation.interpretation[0].coding[x].display (separated by \<br />)
- Reference Range: Observation.referenceRange[x]{ text || low.value && “-“ && high.value} (concatenate with comma, e.g. x, y, z)
- Comments: Observation.note[x].text (separated by \<br />)
- Date: Observation.effectiveDateTime || Observation.effectivePeriod.start
 
TABLE 2: Diagnostic Results: Diagnostic Reports
- Code: DiagnosticReport.code.text || DiagnosticReport.code.coding[x].display (separated by \<br />)
- Date: DiagnosticReport.effectiveDateTime || DiagnosticReport.effectivePeriod.start
 
Social History:
- Code: Observation.code.text || Observation.code.coding[x].display (separated by \<br />)
- Result: Observation.valueQuantity || Observation.valueDateTime || Observation.valueCodeableConcept.text || Observation.valueCodeableConcept.coding[x].display (separated by \<br />) || Observation.valueString
- Unit: Observation.valueQuantity.unit
- Comments: Observation.note[x].text (separated by \<br />)
- Date: Observation.effectiveDateTime || Observation.effectivePeriod.start
 
Vital Signs:  
- Code: Observation.code.text || Observation.code.coding[x].display (separated by \<br />)
- Result: Observation.valueQuantity || Observation.valueDateTime || Observation.valueCodeableConcept.text || Observation.valueCodeableConcept.coding[x].display (separated by \<br />) || Observation.valueString
- Unit: Observation.valueQuantity.unit
- Interpretation: Observation.interpretation[0].text || Observation.interpretation[0].coding[x].display (separated by \<br />)
- Comments: Observation.note[x].text (separated by \<br />)
- Date: Observation.effectiveDateTime || Observation.effectivePeriod.start