---
title: 21st Century Cures Act
parent: Legal
---

- <https://onc-healthit.github.io/api-resource-guide/404-conditions-maintenance/#applicability>
- <https://www.federalregister.gov/documents/2020/05/01/2020-07419/21st-century-cures-act-interoperability-information-blocking-and-the-onc-health-it-certification>

>By December 31, 2022, all Certified Health Information Technology (i.e., EHR vendors) must have the new HL7 FHIR API capability and make information in USCDI Version 1 available to their customers.


<https://www.healthit.gov/buzz-blog/healthit-certification/an-upcoming-milestone-in-our-interoperability-journey>
Century Cures Act, [certified electronic medical record systems are now required to provide open FHIR API endpoints to their customers and patients](https://www.healthit.gov/buzz-blog/healthit-certification/an-upcoming-milestone-in-our-interoperability-journey). FHIR is a HL7 standard that defines data primitives in healthcare and allows medical systems to communicate using these data primitives. In short, FHIR defines a standardized way for external programs to communicate with these health systems to access patient data.
> <https://meremedical.co/blog/what-is-mere-medical/>


https://www.opennotes.org/onc-federal-rule/


Starting on October 6, 2022, the **definition** of electronic health information (EHI) in the 21st Century Cures Act will expand beyond the United States Core Data for Interoperability (USCDI) Version 1 to **all** electronic Protected Health Information (ePHI) that **a patient has the right to access** under the Health Insurance Portability and Accountability Act (HIPAA).

**Background:** In the HIPAA Privacy Rule, protected health information (PHI) is considered **any** identifiable health information used, maintained, stored, or transmitted by a covered entity.

A **covered entity health care provider** is one that bills an insurance company for services provided to **any** patient. Covered entities include health plans and healthcare clearinghouses. Note: The Information Blocking Rule **also** applies to **some** organizations that are NOT covered entities; however, it is not applicable to all covered entities

Starting on October 6, 2022, instead of being limited to the USCDI Version 1, the definition of EHI will now include **all** information in a Designated Record Set, as defined under HIPAA.

In other words, EHI **will not be limited to the specific data classes listed in the USCDI** and will also consist of **medical and payment records about a patient** and any information of a type that may be used to make decisions about individuals, including patients. For actors covered by the information blocking rules, all ePHI in a Designated Record Set is considered to be EHI and subject to those rules.

**EHI could include:**

-   Medical records and billing records about individuals maintained by or for a covered healthcare provider;
-   Enrollment, payment, claims adjudication, and case or medical management record systems; or
-   Other records that are used, in whole or in part, by or for the covered entity to make decisions about individuals.

![Understanding the scope of Electronic Health Information (EHI) for the Purposes of the Information Blocking Definition](https://www.opennotes.org/wp-content/uploads/2022/07/understanding_EHI_for_InfoBlocking-535x317.png)

Understanding the scope of Electronic Health Information (EHI) for the Purposes of the Information Blocking Definition

**More information about about EHI and ePHI can be found at HealthIT.gov**, and downloaded as PDFs:

-   [Understanding Electronic Health Information (EHI)](https://www.healthit.gov/cures/sites/default/files/cures/2021-12/Understanding_EHI.pdf) [PDF]
-   [Understanding the scope of Electronic Health Information for the purposes of the Information Blocking Definition](https://www.healthit.gov/cures/sites/default/files/cures/2021-12/Understanding_EHI-Scope-Diagram.pdf) [PDF]



### Note types that must be shared between April 2021-October 2022

The eight (8) types of clinical notes that must be shared are outlined in the United States Core Data for Interoperability (USCDI), and include:

-   consultation notes
-   discharge summary notes
-   history & physical
-   imaging narratives
-   laboratory report narratives
-   pathology report narratives
-   procedure notes
-   progress notes

[View the full USCDI](https://www.healthit.gov/isa/united-states-core-data-interoperability-uscdi).


https://www.healthit.gov/sites/default/files/2018-12/LeveragingHITtoPromotePatientAccess2.pdf


---
While the Cures Act specifies penalties for health IT developers, HINs and HIEs, Congress left it up to the Department of Health and Human Services (HHS) to issue regulations on “disincentives” and enforcement policies for physicians. At this time, HHS has not yet released information on physician penalties.

Information blocking practices can be an Actor’s acts or omissions—essentially anything that interferes with the access, exchange or use of EHI. However, just because an action interferes with the access, exchange or use of EHI does not mean the practice is automatically considered an information blocking violation—facts and circumstances unique to each action should be considered. For instance, physician Actors must have the required **_knowledge and intent_** to interfere with access, exchange or use of EHI. Information blocking practices may include but are not limited to:

-   Limiting or restricting the interoperability of health IT;
-   Implementing health IT in ways that are likely to restrict the access, exchange or use of EHI;
-   Acts that lead to fraud, waste or abuse or impede care delivery enabled by health IT (for example, modifying EHR data reported to federal payment programs such as MIPS) and
-   Having the capability to provide same-day access to EHI in a form and format requested by a patient or a patient’s health care provider but taking several days to respond.

Physicians may implicate the information blocking rule if they knowingly take actions that interfere with exchange, access and use of EHI, even if no harm materializes.

https://www.ama-assn.org/practice-management/digital/patient-access-playbook-information-blocking

https://www.ama-assn.org/system/files/2020-02/patient-records-playbook.pdf

> If a patient requests that you share information  
through an app, you are required to do so under  
HIPAA if you have the technology to do so. Your EHR’s  
API should allow the app to connect and receive  
information securely. You are not responsible for  
whether the app is a “good one,” including whether  
it has appropriate privacy and security in place. If the  
patient’s information is breached once stored within  
the app, you are not responsible.


![](/img/Pasted%20image%2020221018215022.png)

https://www.particlehealth.com/blog/cures-act-timeline


> Publication of “FHIR service base URLs” (sometimes also referred to as “FHIR
endpoints”) - A FHIR service base URL cannot be withheld by an actor as it (just like many other
technical interfaces) is necessary to enable the access, exchange, and use of EHI
>
> https://www.healthit.gov/sites/default/files/page2/2020-03/ONC21stCenturyCuresActFinalRuleOverview.pdf



https://www.darenasolutions.com/cures-act-for-healthcare-providers

## Information Blocking Claims: By the Numbers

ONC has greatly simplified the [process of submitting](https://www.healthit.gov/sites/default/files/page2/2021-11/Information-Blocking-Portal-Process.pdf) an Information Blocking Claim. Information blocking claims can be submitted online through [ONC’s Report Information Blocking Portal](https://healthit.gov/report-info-blocking). The HHS OIG has the authority to investigate claims of possible information blocking across all types of actors: health care providers, health information networks and health information exchanges, and health IT developers of certified health IT.

The Information Blocking claims and information received by ONC in connection with a claim or suggestion of possible information blocking are generally protected from disclosure as specified by the Cures Act. Claims can be submitted anonymously as well.

ONC is tracking Information Blocking Claims starting from April 5, 2021 and now publishing the results monthly. There has been about a **20% increase in the number of validated Claims** submitted from the end of 2021 to August 31, 2022.

[

![Information-Blocking-Claims](https://images.squarespace-cdn.com/content/v1/5c3ce7fc2714e564a6af4b46/e864333c-262c-4a50-baa4-d11992d3b247/Information-Blocking-Claims.jpg)



](https://www.healthit.gov/data/quickstats/information-blocking-claims-numbers)

![Claims-Count-Types-of-Claimant](https://images.squarespace-cdn.com/content/v1/5c3ce7fc2714e564a6af4b46/df76fb79-b0c1-4365-a151-cecd77b898d6/Claims-Count-Types-of-Claimant.jpg)

![claims-count-potential-actor](https://images.squarespace-cdn.com/content/v1/5c3ce7fc2714e564a6af4b46/a305bad1-c6d8-4aff-bef5-484817d5cba3/claims-count-potential-actor.png)

- About a 20% increase in the number of claims has been recorded from the end of 2021 to August 31, 2022.
    

- The number of patients submitting Information Blocking Claims increased by 20% from the end of 2021 to August of 2022.
    
- **More than 75% of the Information Blocking Claims are filed on providers.**
    
- The number of **Claims against providers went up about 35%** from the end of 2021 to August of 2022.