---
title: Patient Data Collection
parent: Technical
---

https://chat.fhir.org/#narrow/stream/179166-implementers/topic/Patient-focused.20record.20creator/near/325989726

> Hi,
>
> I'm working on a [patient-focused open-source healthcare application](https://github.com/fastenhealth/fasten-onprem "https://github.com/fastenhealth/fasten-onprem"). It currently integrates with 1000's of healthcare institutions, allowing users to automatically retrieve their medical records from their institution's EMR. 
> 
> However, we've received constant feedback that users would also like the ability to create records themselves:
> - their institution may not be supported by Fasten
> - their institution may be international (and not have a patient-accessible portal)
> - they have old records that no longer exist
> - they have relevant medical data that has never been tracked by an institution
> - etc. 
> 
> Since our system already uses and understands FHIR documents, I'd like to store patient manually-created documents in the same format, however [FHIR editors](http://docs.smarthealthit.org/fred/) seem complicated, requiring patients to understand the FHIR spec.
> 
> I know this is unlikely, but I'm hoping you may be aware of known/popular mechanisms for generating FHIR resources from patient information -- ideally open-source?
> 
> - a UI library that generates "simple" forms for each (or multiple) FHIR resource type?
> - using the FHIR Questionnaire resource/wizard for prompting users for their medical information?
> - an ML based system to parse free-text into records. 
> - a simple DSL (similar to FSH) that can generate FHIR records. 
> - a question/answer style chatbot for generating records


## answer from Josh Mandel

> Depending on your key use cases (e.g., allowing patients to enter meds or allergies from a non FHIR enabled source, vs allowing full import of historical paper based records), there are some different choices.
> 
> GPT-3.5 models do a pretty reasonable job of turning free text into specific FHIR resources, but it still takes finesse to make these actually correct.
> 
> Some very targeted UX for Allergies, Meds, and Conditions would probably be more usable than a generic StructureDefinition backed form interface. 
> 
> That said, I haven't seen a good take on a usable SD driven generic form UX. It seems like a broadly useful component. https://gitlab.com/genfhi/genfhi may have useful bits (I haven't explored), http://docs.smarthealthit.org/fred is too dev oriented... @**Brian Postlethwaite** have you seen or explored anything like this UI with the Forms Lab, or translate of SDs into Questionnaires so generic tooling like https://lhcforms.nlm.nih.gov/lhcforms could render them?


https://lhcforms.nlm.nih.gov/lhcforms
[https://gitlab.com/genfhi/genfhi](https://gitlab.com/genfhi/genfhi "https://gitlab.com/genfhi/genfhi")

