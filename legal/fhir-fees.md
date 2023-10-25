---
title: FHIR Fees
parent: Legal
---

Conversation was found on - <https://chat.fhir.org/#narrow/stream/179166-implementers/topic/Charging.20fees.20for.20FHIR.20API>


> Q. In the United States, I understand that the ONC allows us to charge a fee for 3rd parties to access our FHIR APIs, especially if it is to offset the costs to support the APIs. For example, if we needed a developer support team to review and triage issues and questions.
>
   Is anyone doing this in practice in the FHIR community in the U.S.A? How has that gone with your 3rd party developers?


Keep in mind that within the United States context, you cannot charge for _patient API access_... although it is permissible 
to charge reasonable and non-discriminatory fees for API usage by clinician facing apps.

I think the details were more around _who_ you can charge and _what_ you can charge for.

My understanding is that you can charge app developers for value added services, and you can charge customers 
(healthcare organizations, not 3rd party app developers) for USCDI / patient access. "Developer support, issue triage, 
and answering questions" are a bit of a grey area. If you have stellar documentation and a working sandbox, than I think 
answering questions could fall under "value added services" and could be charged for. However, if your documentation is 
lacking and you have no test sandbox, then answering questions is probably essential for using your APIs, and you probably 
can't charge? Issue triage _may_ fall under the normal work you'd do to maintain a product, so likely would be 
covered by the fees you'd bill the health system.

Our _goal_ is to not have to answer questions or provide dev support to USCDI app developers. But since the first pass 
(or first dozen passes) of documentation isn't perfect, we answer (for free) questions from app developers and use that 
process to help drive documentation improvements, so we get fewer questions over time.

Also, based on my experience, often we get questions from app developers that start with USCDI, but quickly move into 
non-USCDI. So you can sometimes jump between 21CCA pricing rules and value added services in the same conversation. It gets fun...

*Special disclaimer: I'm not an expert on the pricing aspect of 21CCA. There are other folks that pay closer attention 
to this to make sure we comply, but I think my comments reflect our general approach.

[170.404 - Application programming interfaces](https://www.federalregister.gov/documents/2020/05/01/2020-07419/21st-century-cures-act-interoperability-information-blocking-and-the-onc-health-it-certification#sectno-reference-170.404 "https://www.federalregister.gov/documents/2020/05/01/2020-07419/21st-century-cures-act-interoperability-information-blocking-and-the-onc-health-it-certification#sectno-reference-170.404")
is the applicable section (the [Cornell Law version](https://www.law.cornell.edu/cfr/text/45/170.404 "https://www.law.cornell.edu/cfr/text/45/170.404") has better formatting). Specifically, section (a)(3).

