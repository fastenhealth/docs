
## Helpful Links

- [ONC HealthIT - 170.315(g)(10) - Standardized API for Patient and Population Services](https://www.healthit.gov/test-method/standardized-api-patient-and-population-services)
- [ONC Health App Use Scenarios & HIPAA(https://www.hhs.gov/sites/default/files/ocr-health-app-developer-scenarios-2-2016.pdf)
- [HTI-1 Final Rule](https://www.federalregister.gov/documents/2024/01/09/2023-28857/health-data-technology-and-interoperability-certification-program-updates-algorithm-transparency-and#p-1250)
	- [ONC HTI-1 Final Rule Overview](https://www.healthit.gov/sites/default/files/page/2024-01/HTI-1%20Final%20Rule%20Overview_Webinar_508.pdf)
- [Information Blocking Exceptions](https://www.healthit.gov/sites/default/files/2024-04/IB_Exceptions_Fact_Sheet_508_0.pdf)

## Do Patient Access Applications need to be HIPAA compliant

> <https://www.hhs.gov/sites/default/files/ocr-health-app-developer-scenarios-2-2016.pdf>

| Scenario                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        | Based on the Facts Presented in the Scenario, Is App Developer a HIPAA Business Associate?                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Consumer downloads a health app to her smartphone that is designed to help her manage a chronic condition. She downloads data from her doctor’s EHR through a patient portal, onto her computer and then uploads it into the app. She also adds her own information to the app.                                                                                                                                                                                                                                                 | **No. Developer is not creating, receiving, maintaining or transmitting protected health information (PHI) on behalf of a covered entity or another business associate.** Instead, the consumer obtains health information from her provider, combines it with health information she inputs, and uses the app to organize and manage that information for her own purposes. There is no indication the provider or a business associate of the provider hired the app developer to provide or facilitate this service.                                                                                 |
| Consumer downloads a health app to her smartphone that is designed to help her manage a chronic condition.Health care provider and app developer have entered into an interoperability arrangement at the consumer’s request that facilitates secure exchange of consumer information between the provider EHR and the app. The consumer populates information on the app and directs the app to transmit the information to the provider’s EHR. The consumer is able to access test results from the provider through the app. | No. Developer is not creating, receiving, maintaining ortransmitting protected health information (PHI) on behalf of a covered entity or another business associate. The interoperability arrangement alone does not create a BA relationship because the arrangement exists to facilitate access initiated by the consumer. The app developer is providing a service to the consumer, at the consumer’s request and on her behalf. The app developer is transmitting data on behalf of the consumer to and from the provider; this activity does not create a BA relationship with the covered entity. |

## Do Patient Access Apps need to sign a BAA with Providers/EHRs?

The HHS has provided the following guidance for requiring BAAs for individual access requests via a third party app.  

See [https://www.hhs.gov/hipaa/for-professionals/privacy/guidance/access-right-health-apps-apis/index.html](https://www.hhs.gov/hipaa/for-professionals/privacy/guidance/access-right-health-apps-apis/index.html)  

> The HIPAA Privacy Rule generally prohibits a covered entity from refusing to disclose ePHI to a third-party app designated by the individual if the ePHI is readily producible in the form and format used by the app.

And just beyond:  

> Q: **Does HIPAA require a covered entity or its EHR system developer to enter into a business associate agreement with an app designated by the individual in order to transmit ePHI to the app?**  
> HIPAA does not require a covered entity or its business associate (e.g., EHR system developer) to enter into a business associate agreement with an app developer that does not create, receive, maintain, or transmit ePHI on behalf of or for the benefit of the covered entity

## Do EHR Developers need to provide a Provider/Endpoint Catalog

> Yes, under the HTI-1 Final Rule, EHR developers are required to publish their customers' service base URL information, which includes FHIR endpoints. This is part of the new and updated standards, implementation specifications, and certification criteria for electronic health records and health information technology modules for certification through the ONC certification program.



## What Developer Documentation must an EHR provide?

From [Paragraph (g)(10)(viii)(A) Documentation – minimum requirements](https://www.healthit.gov/test-method/standardized-api-patient-and-population-services)

> Technical outcome – The API(s) must include complete accompanying documentation that contains, at a minimum: 
> (_1_) API syntax, function names, required and optional parameters supported and their data types, return variables and their types/structures, exceptions and exception handling methods and their returns; 
> (_2_) The software components and configurations that would be necessary for an application to implement in order to be able to successfully interact with the API and process its response(s); and 
> (_3_) All applicable technical requirements and attributes necessary for an application to be registered with a Health IT Module’s authorization server.




## Sandbox for Testing


### How can I file an Information Blocking 