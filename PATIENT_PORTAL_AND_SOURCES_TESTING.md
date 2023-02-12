

> It’s an ONC Cures Rule maintenance of certification requirement for certification criterion  Standardized API for Patient and Population Services 170.315(g)(10) for certified API  developers to publish service base URLs for all customers in a machine-readable format.
> 
> [Regulatory Text: 45 CFR 170.404(b)(2) ](https://ecfr.federalregister.gov/current/title-45/subtitle-A/subchapter-D/part-170/subpart-Dp-170.404(b)(2))
> Certified API Developers must publish service base URLs for all Health IT Modules certified to § 170.315(g)(10) that can be used by patients to access their EHI.  
> Certified API Developers must publicly publish service base URLs for all customers in a machine-readable format at no charge.  
> 
> As discussed in section VIII.C.6.c of the ONC Cures Act Final Rule, API Information  Sources who locally manage their FHIR servers without Certified API Developer  assistance cannot refuse to provide to Certified API Developers the FHIR service  base URL(s) that is/are necessary for patients to use to access their EHI. Equally,  pursuant to this Maintenance of Certification requirement, they would be  required to publish the FHIR service base URLs they centrally manage on behalf  of API Information Sources.
> 
> https://www.healthit.gov/sites/default/files/2021-12/Lantern-webinar_508.pdf





# EMR Vendors & Market Share





https://github.com/onc-healthit/lantern-back-end/tree/939e4b3979ce4e37f9473fdc8b1e58b8e552a6d7/db

https://github.com/onc-healthit/lantern-back-end/blob/939e4b3979ce4e37f9473fdc8b1e58b8e552a6d7/resources/dev_resources/CHPLEndpointResourcesList.json
https://github.com/onc-healthit/lantern-back-end/blob/939e4b3979ce4e37f9473fdc8b1e58b8e552a6d7/resources/prod_resources/CHPLEndpointResourcesList.json
https://github.com/onc-healthit/lantern-back-end/blob/939e4b3979ce4e37f9473fdc8b1e58b8e552a6d7/resources/prod_resources/CHPLProductsInfo.json

# FHIR Sandboxes
- https://sandbox.logicahealth.org/fastenhealth/apps
- https://github.com/sync-for-science/procure-wip/blob/f234eb1d4f7121da31baf1809be8f5726210bc99/public/config/sandbox_endpoints.json#L84
- https://developer.veradigm.com/Fhir/FHIR_Sandboxes#tw

# EPIC SOURCES


https://hackmd.io/@argonaut


FHIR Endpoint Discovery
- https://groups.google.com/g/smart-on-fhir/c/X1zRsk43Wnk
- https://groups.google.com/g/smart-on-fhir/c/0tn4qAsWNCQ
- http://community.fhir.org/t/list-of-production-fhir-endpoint-api-urls/2136
- https://chat.fhir.org/#narrow/stream/252301-Endpoint-Discovery
- https://lantern.healthit.gov/?tab=dashboard_tab
- https://chpl.healthit.gov/#/search
- https://github.com/the-commons-project/vci-directory/blob/main/vci-issuers.json


[patient app registration-who's misinformed at the ONC Forum?](https://chat.fhir.org/#narrow/stream/179262-patient-empowerment/topic/patient.20app.20registration-who's.20misinformed.20at.20the.20ONC.20Forum.3F "Narrow to stream "patient empowerment", topic "patient app registration-who's misinformed at the ONC Forum?"")

Here is our general experience for open developer environments. The problem is essentially endpoint discovery and whitelisting. Please note that not all vendors are included below. However, OneRecord is patiently waiting for ALL endpoints to be published by ALL vendors with no whitelisting :)

Epic: You get a single set of creds (client ID and secret) to connect to all Epic sites. All endpoints published. ( This is the easiest method for patient-facing apps.)

Cerner: You get a single set of creds (client ID and secret) to connect to all Cerner sites (like Epic) BUT whitelisting is required.

eCW: You get a single set of creds (client ID and secret) to connect to all eCW sites (Like Cerner) BUT whitelisting is required.

Allscripts: You get different creds (client ID and secret) for each client to connect to Allscripts sites AND whitelisting is required.

Meditech: You get different creds (client ID and secret) for each client to connect to Meditech sites (like Allscripts) AND whitelisting is required.

NextGen: You get different creds (client ID and secret) for each client to connect to NextGen sites AND whitelisting is required.

Athena: To date does not support 3 Legged OAUTH

Ultimately you are going to see some sort of configuration that follows the patterns above and as @Debi Willis said "it’s an Olympic exercise" to find the right stakeholder to get whitelisted...even at the patient request.


https://chat.fhir.org/#narrow/stream/179262-patient-empowerment/topic/patient.20app.20registration-who's.20misinformed.20at.20the.20ONC.20Forum.3F


# FHIR Source Directories
- https://1up.health/fhir-endpoint-directory/1
- https://www.cmscompliancetracker.com/?page_id=89
- [https://github.com/flexpa/sero/issues/78](https://github.com/flexpa/sero/issues/78)
- https://www.cmscompliancetracker.com/
- https://www.cloverhealth.com/en/developers
- https://www.alignmenthealth.com/api
- https://touchstone.aegis.net/touchstone/
- https://portal.particlehealth.com/signup/
- https://1up.health/docs/start/fhir-test-credentials
- https://support.apple.com/en-us/HT208647\
- ALL MyChart should be supported via Epic integration - https://open.epic.com/Tutorial/PatientAuthentication?whereFrom=MyChart
- https://download.cms.gov/nppes/NPI_Files.html
- https://carequality.org/active-sites-search/
- https://lantern.healthit.gov/?tab=dashboard_tab


## Example Datasets / Synthetic Data
- [https://synthetichealth.github.io/synthea/](https://synthetichealth.github.io/synthea/)
- [http://docs.smarthealthit.org/dstu2-examples/](http://docs.smarthealthit.org/dstu2-examples/)
- [https://github.com/hapifhir/fhir-tutorial/blob/master/Transactions/lesson.md](https://github.com/hapifhir/fhir-tutorial/blob/master/Transactions/lesson.md)
- [https://physionet.org/content/mimic-iv-fhir-demo/2.0/](https://physionet.org/content/mimic-iv-fhir-demo/2.0/ "https://physionet.org/content/mimic-iv-fhir-demo/2.0/")
- https://www.mdpi.com/2079-9292/11/8/1199


http://hl7.org/fhir/us/davinci-pdex/index.html
https://github.com/Open-Health-Manager/standard-patient-health-record-ig
https://open-health-manager.github.io/standard-patient-health-record-ig/
https://confluence.hl7.org/display/PE/Patient+Empowerment+Home
https://confluence.hl7.org/display/PA


https://launch.smarthealthit.org/?auth_error=&fhir_version_2=r4&iss=&launch_pt=1&launch_url=&patient=&prov_skip_auth=1&provider=&pt_skip_auth=1&public_key=&sde=&token_lifetime=15&user_pt=


