# Does Fasten Self-hosted need to be HIPAA Compliant

Hey /r/healthit,

I'm a software engineer developing an [application intended to act as a personal health/medical record (PHR/PMR) aggregator](https://www.reddit.com/r/selfhosted/comments/xj9rx7/introducing_fasten_a_selfhosted_personal/) -- allowing users retrieve their data from multiple healthcare providers (insurance companies, hospital networks, clinics, laboratories) across multiple industries (vision, dental, medical) -- and display it all in one dashboard, while storing the data on a device under their control.

There's a bunch of technologies I'm using under the hood to make this work (FHIR, Smart-on-FHIR, PKCE, etc) but here's what I'm interested in confirming with /r/healthit's help.

My understanding is that my application would not be covered under HIPAA:

- users selfhost the application on their own hardware (laptop, computer, home-server)
- patients are requesting their own data (under [HIPAA/21st Century Cures Act - Patient Access right](https://www.healthit.gov/sites/default/files/2018-12/LeveragingHITtoPromotePatientAccess2.pdf)) and requesting that it be directly transferred to a (non-compliant) application of their choice (my app running on their device), under the [Cures Act Final Rule](https://www.healthit.gov/sites/default/files/page2/2020-03/TheONCCuresActFinalRule.pdf)
- the app running on their device directly communicates with the healthcare provider to retrieve the patient's health record, **the healthcare data does not ever transit a server under my (the app developer's) control.**


There is some additional nuance here related to the authentication flow, but I can ask that as a separate follow-up question.

At this point I'd just like to confirm my understanding that **an application storing a patients data on their own device, at the patients request, would not fall under HIPAA compliance.**

> https://www.reddit.com/r/healthIT/comments/xs3bk5/hipaa_compliance_requirements_for_3rd_party/
> https://www.reddit.com/r/hipaa/comments/xs349e/hipaa_compliance_requirements_for_3rd_party/


# Responses 

> https://www.hhs.gov/sites/default/files/ocr-health-app-developer-scenarios-2-2016.pdf

| Scenario | Based on the Facts Presented in the Scenario, Is App Developer a HIPAA Business Associate? |
| --- | --- |
| Consumer downloads a health app to her smartphone that is designed to help her manage a chronic condition. She downloads data from her doctor’s EHR through a patient portal, onto her computer and then uploads it into the app. She also adds her own information to the app. | No. Developer is not creating, receiving, maintaining or transmitting protected health information (PHI) on behalf of a covered entity or another business associate. Instead, the consumer obtains health information from her provider, combines it with health information she inputs, and uses the app to organize and manage that information for her own purposes. There is no indication the provider or a business associate of the provider hired the app developer to provide or facilitate this service. |
| Consumer downloads a health app to her smartphone that is designed to help her manage a chronic condition.Health care provider and app developer have entered into an interoperability arrangement at the consumer’s request that facilitates secure exchange of consumer information between the provider EHR and the app. The consumer populates information on the app and directs the app to transmit the information to the provider’s EHR. The consumer is able to access test results from the provider through the app. | No. Developer is not creating, receiving, maintaining ortransmitting protected health information (PHI) on behalf of a covered entity or another business associate. The interoperability arrangement alone does not create a BA relationship because the arrangement exists to facilitate access initiated by the consumer. The app developer is providing a service to the consumer, at the consumer’s request and on her behalf. The app developer is transmitting data on behalf of the consumer to and from the provider; this activity does not create a BA relationship with the covered entity.

f you are an app vendor, and you are not already a covered entity, you should consider the following
questions in determining whether or not you may be a business associate – i.e., an entity that creates,
receives, maintains or transmits protected health information (PHI) on behalf of a covered entity or
business associate:
- Does your health app create, receive, maintain, or transmit identifiable information?
- Who are your clients? How are you funded?
  - Are your clients covered entities? e.g.,
    - hospitals, doctor’s offices, clinics, pharmacies, or other health care providers who conduct electronic transactions;
    - health insurance issuers; health or wellness program related to a health plan offered by an employer
  - Were you hired by, or are you paid for your service or product by, a covered entity? Or another business contracted to a covered entity?
  - Does a covered entity (or a business associate acting on its behalf) direct you to create, receive, maintain or disclose information related to a patient or health plan member?

If you are only offering services directly to and collecting information for or on behalf of consumers, and
not on behalf a provider, health plan or health care clearinghouse, you are not likely to be subject to
HIPAA as either a covered entity or business associate.

- Is your app independently selected by a consumer?
- Does the consumer control all decisions about whether to transmit her data to a third party,  such as to her health care provider or health plan?
- Do you have no relationship with that third party entity (other than an interoperability relationship)?


# Further Reading

> This was why the CURES act also established TEFCA, although the act didn't go as far as adopting TEFCA. It did leave the opportunity for any federal agency taking health data to require the use of TEFCA, and hopefully CMS does that.
> https://www.reddit.com/r/hipaa/comments/xs349e/hipaa_compliance_requirements_for_3rd_party/iqjkxo8/

> https://www.hhs.gov/hipaa/for-professionals/special-topics/health-apps/index.html
> https://www.healthit.gov/topic/information-blocking
> https://www.hhs.gov/hipaa/for-professionals/privacy/guidance/access-right-health-apps-apis/index.html
