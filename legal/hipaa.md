---
title: HIPAA
parent: Legal
---

# HIPAA/HITRUST BAA
- https://learn.microsoft.com/en-us/azure/compliance/offerings/offering-hipaa-us
    > AFAIK (and a cursory read of the terms confirms this) that the Microsoft BAA applies to you automatically via the product terms so long as you are either a CE or BA. Of course, if you don’t like the terms of the default BAA that’s up to you.  But it’s basically free and doesn’t require new paperwork. Make sure to confirm that your services are covered:
- https://aws.amazon.com/compliance/hipaa-compliance/
- https://aws.amazon.com/compliance/hipaa-eligible-services-reference/

# Policy Files
- <https://github.com/truevault/hipaa-compliance-developers-guide>
- <https://github.com/HealthDecision/policies-ref-fork>
- <https://github.com/lumahealthhq/policy>
- <https://github.com/MolecularMatch/training>
- <https://www.hhs.gov/sites/default/files/ocr/privacy/hipaa/understanding/special/healthit/phrs.pdf>

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

> - <https://www.reddit.com/r/healthIT/comments/xs3bk5/hipaa_compliance_requirements_for_3rd_party/>
> - <https://www.reddit.com/r/hipaa/comments/xs349e/hipaa_compliance_requirements_for_3rd_party/>


# Responses 

> <https://www.hhs.gov/sites/default/files/ocr-health-app-developer-scenarios-2-2016.pdf>

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

---
If you are specifically looking for your obligations under 21st Century Cures, you are probably looking for information about Information Blocking which is overseen by the Office of the National Coordinator of Health Information Technology (ONC). There is more information here:

<https://www.healthit.gov/topic/information-blocking>

The newer, better, nicer HHS is very cooperative with industry stakeholders and you can reach out to them directly once you've attempted to digest the available published materials. Don't be surprised if you get answers such as "OCR is responsible for enforcing that regulation and we can't speak to what they would do."

Edit: Added ( ) for clarity.

> <https://www.reddit.com/r/healthIT/comments/xs3bk5/hipaa_compliance_requirements_for_3rd_party/iqinzxw/>

---

If you haven't found a system to partner with, do that, you'll get more than you want to know about how to secure this.

Also, if you haven't started looking at the trusted exchange framework and common agreement, I suggest you look at that to better facilitate gathering this information. It will be a few more years before the FHIR integration roadmap is implemented. More will be announced around this framework towards the end of the year.

At the end of the day, while there is a need for something like this, I don't know if you fully understand the complexities involved in getting this kind of information. It is a huge clusterfuck of crazy. This is why a lot of healthcare start-ups struggle with this industry is that you have to deal with data quality and silos that come with decades of baggage.

> <https://www.reddit.com/r/hipaa/comments/xs349e/hipaa_compliance_requirements_for_3rd_party/iqj67sn/>

# Further Reading

> This was why the CURES act also established TEFCA, although the act didn't go as far as adopting TEFCA. It did leave the opportunity for any federal agency taking health data to require the use of TEFCA, and hopefully CMS does that.
> <https://www.reddit.com/r/hipaa/comments/xs349e/hipaa_compliance_requirements_for_3rd_party/iqjkxo8/>
>
> - <https://www.hhs.gov/hipaa/for-professionals/special-topics/health-apps/index.html>
> - <https://www.healthit.gov/topic/information-blocking>
> - <https://www.hhs.gov/hipaa/for-professionals/privacy/guidance/access-right-health-apps-apis/index.html>



# Can Providers/EHR platforms require a BAA?

See [https://www.hhs.gov/hipaa/for-professionals/privacy/guidance/access-right-health-apps-apis/index.html#:~:text=The%20HIPAA%20Privacy%20Rule%20generally%20prohibits%20a%20covered%20entity%20from%20refusing%20to%20disclose%20ePHI%20to%20a%20third%2Dparty%20app%20designated%20by%20the%20individual%20if%20the%20ePHI%20is%20readily%20producible%20in%20the%20form%20and%20format%20used%20by%20the%20app](https://www.hhs.gov/hipaa/for-professionals/privacy/guidance/access-right-health-apps-apis/index.html#:~:text=The%20HIPAA%20Privacy%20Rule%20generally%20prohibits%20a%20covered%20entity%20from%20refusing%20to%20disclose%20ePHI%20to%20a%20third%2Dparty%20app%20designated%20by%20the%20individual%20if%20the%20ePHI%20is%20readily%20producible%20in%20the%20form%20and%20format%20used%20by%20the%20app "https://www.hhs.gov/hipaa/for-professionals/privacy/guidance/access-right-health-apps-apis/index.html#:~:text=The%20HIPAA%20Privacy%20Rule%20generally%20prohibits%20a%20covered%20entity%20from%20refusing%20to%20disclose%20ePHI%20to%20a%20third%2Dparty%20app%20designated%20by%20the%20individual%20if%20the%20ePHI%20is%20readily%20producible%20in%20the%20form%20and%20format%20used%20by%20the%20app").

> The HIPAA Privacy Rule generally prohibits a covered entity from refusing to disclose ePHI to a third-party app designated by the individual if the ePHI is readily producible in the form and format used by the app.

And just beyond:

> 5. Q: Does HIPAA require a covered entity or its EHR system developer to enter into a business associate agreement with an app designated by the individual in order to transmit ePHI to the app?

> HIPAA does not require a covered entity or its business associate (e.g., EHR system developer) to enter into a business associate agreement with an app developer that does not create, receive, maintain, or transmit ePHI on behalf of or for the benefit of the covered entity


# Endpoint Catalog - HTI-1
- https://www.healthit.gov/sites/default/files/page/2023-12/HTI-1_Gen-Overview_factsheet_508.pdf
