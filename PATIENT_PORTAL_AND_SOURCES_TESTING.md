


# EMR Vendors & Market Share

>[full list of CURES Act compliant EHR systems](https://chpl.healthit.gov/#/search) 
>- 170.315 (g)(10): Standardized API for Patient and Population Services (Cures Update)

- Epic: 32.9%
	- [x] https://open.epic.com/MyApps/Endpoints
	- [x] https://open.epic.com/Endpoints/R4 ✅ 2023-01-12
	- [ ] https://fhir.epic.com/Developer/Management?id=21498
	- [ ] https://www.mychart.com/LoginSignup
	- status: prod access granted
- Cerner: 24.4%
	- [x] https://github.com/cerner/ignite-endpoints/blob/main/millennium_patient_r4_endpoints.json
	- status: prod access granted
- Meditech: 16.7% (350)
	- [ ] https://fhir.meditech.com/explorer/endpoints
	- status: need to request new creds (email sent)
- CPSI: 8.7%
	- https://unify-developer.chbase.com/?page=FHIRAPI
	- unifyURL = "[https://unify-developer.chbase.com/?page=FHIRAPI](https://unify-developer.chbase.com/?page=FHIRAPI)"
	- status: --
- Allscripts: 4.3%
	- https://open.allscripts.com/fhirendpoints
	- status: sandbox access granted - testing failed
- Medhost: 3.1%
	- status: --
- Cigna
	- [ ]
	- status: fill out form
- CareEvolution
	- status: sandbox access - no production access available (site by site required)
- eClinicalWorks - healow.com
	- status: [submitted api request](https://www.eclinicalworks.com/products-services/interoperability/provider-centric-apps/)
- NextGenHealthcare (4036)
	- [ ] https://www.nextgen.com/api/practice-search
	- status: sent email requesting client
- Anthem
	- [x] https://patient360.anthem.com/P360Member/fhir/endpoints
	- status: prod


https://github.com/onc-healthit/lantern-back-end/blob/939e4b3979ce4e37f9473fdc8b1e58b8e552a6d7/endpointmanager/pkg/chplendpointquerier/chplendpointquerier.go

- MedHostURL = "https://api.mhdi10xasayd.com/medhost-developer-composition/v1/fhir-base-urls.json"
- NextGenURL = "https://nextgen.com/api/practice-search"
- CanvasURL = "https://docs.canvasmedical.com/reference/service-base-urls"
- AllScriptsURL = "https://open.allscripts.com/fhirendpoints"
- AlteraURL = "https://open.allscripts.com/fhirendpoints"
- EpicURL = "https://open.epic.com/MyApps/Endpoints"
- MeditechURL = "https://home.meditech.com/en/d/restapiresources/pages/apidoc.htm"
- MeditechURL = "https://fhir.meditech.com/explorer/endpoints"
- DocsAthenaURL = "https://docs.athenahealth.com/api/base-fhir-urls"
- MyDataAthenaURL = "https://mydata.athenahealth.com/home"
- OneMedicalURL = "https://apidocs.onemedical.io/fhir/overview/"

- trimedtechURL = "[https://www.trimedtech.com/Documentation/FHIRAPI/FHIRAPI.html](https://www.trimedtech.com/Documentation/FHIRAPI/FHIRAPI.html)"
- trimedtechv8URL = "[https://www.trimedtech.com/Documentation/FHIRAPI/V8FHIRAPI.html](https://www.trimedtech.com/Documentation/FHIRAPI/V8FHIRAPI.html)"
- cernerR4URL = "[https://github.com/cerner/ignite-endpoints/blob/main/soarian_patient_r4_endpoints.json](https://github.com/cerner/ignite-endpoints/blob/main/soarian_patient_r4_endpoints.json)"
- techCareURL = "[https://devportal.techcareehr.com/Serviceurls](https://devportal.techcareehr.com/Serviceurls)"
- carefluenceURL = "[https://carefluence.com/carefluence-fhir-endpoints/](https://carefluence.com/carefluence-fhir-endpoints/)"
- abeoSolutionsURL = "[https://www.crystalpm.com/FHIRServiceURLs.csv](https://www.crystalpm.com/FHIRServiceURLs.csv)"
- practiceSuiteURL = "[https://academy.practicesuite.com/fhir-server-links/](https://academy.practicesuite.com/fhir-server-links/)"
- bizmaticsURL = "[https://prognocis.com/fhir/index.html](https://prognocis.com/fhir/index.html)"
- indianHealthServiceURL = "[https://www.ihs.gov/cis/](https://www.ihs.gov/cis/)"
- geniusSolutionsURL = "[https://gsehrwebapi.geniussolutions.com/Help/html/ServiceUrl.html](https://gsehrwebapi.geniussolutions.com/Help/html/ServiceUrl.html)"
- assureCareURL = "[https://ipatientcare.com/onc-acb-certified-2015-edition/](https://ipatientcare.com/onc-acb-certified-2015-edition/)"
- intelichartURL = "[https://fhirtest.intelichart.com/Help/BaseUrl](https://fhirtest.intelichart.com/Help/BaseUrl)"
- healthCare2000URL = "[https://www.provider.care/FHIR/MDVitaFHIRUrls.csv](https://www.provider.care/FHIR/MDVitaFHIRUrls.csv)"
- firstInsightURL = "[https://www.first-insight.com/maximeyes_fhir_base_url_endpoints/](https://www.first-insight.com/maximeyes_fhir_base_url_endpoints/)"
- healthSamuraiURL = "https://cmpl.aidbox.app/smart"
- triarqURL = "https://fhir.myqone.com/Endpoints"
- napchareURL = "https://devportal.techcareehr.com/Serviceurls"
- goldblattURL = "https://www.goldblattsystems.com/apis"
- cyfluentURL = "https://app.swaggerhub.com/apis-docs/Cyfluent/ProviderPortalApi/3.3#/FHIR/fhir"
- mphrxURL = "https://www.mphrx.com/fhir-service-base-url-directory/"
- meridianURL = "https://api-datamanager.carecloud.com:8081/fhirurl"
- qualifactsURL = "https://qualifacts.com/api-documentation/"
- medinfoengineeringURL = "https://docs.webchartnow.com/resources/system-specifications/fhir-application-programming-interface-api/endpoints/"
- relimedsolutionsURL = "https://help.relimedsolutions.com/fhir/fhir-service-urls.csv"
- eclinicalworksURL = "https://fhir.eclinicalworks.com/ecwopendev"
- integraconnectURL = "https://www.integraconnect.com/certifications/"
- streamlinemdURL = "https://patientportal.streamlinemd.com/FHIRReg/Practice%20Service%20based%20URL%20List.csv"
- bridgepatientportalURL = "https://bridgepatientportal.docs.apiary.io/#/introduction/fhir-bridge-patient-portal/fhir-endpoints"
- medicalmineURL = "https://www.charmhealth.com/resources/fhir/index.html#api-endpoints"
- microfourURL = "https://oauth.patientwebportal.com/Fhir/Documentation#serviceBaseUrls"
- magilenenterprisesURL = "https://www.qsmartcare.com/api-documentation.html"

https://github.com/onc-healthit/lantern-back-end/tree/939e4b3979ce4e37f9473fdc8b1e58b8e552a6d7/db

https://github.com/onc-healthit/lantern-back-end/blob/939e4b3979ce4e37f9473fdc8b1e58b8e552a6d7/resources/dev_resources/CHPLEndpointResourcesList.json
https://github.com/onc-healthit/lantern-back-end/blob/939e4b3979ce4e37f9473fdc8b1e58b8e552a6d7/resources/prod_resources/CHPLEndpointResourcesList.json
https://github.com/onc-healthit/lantern-back-end/blob/939e4b3979ce4e37f9473fdc8b1e58b8e552a6d7/resources/prod_resources/CHPLProductsInfo.json

# FHIR Sandboxes
- https://sandbox.logicahealth.org/fastenhealth/apps
- https://confluence.hl7.org/display/FHIR/Public+Test+Servers
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



http://hl7.org/fhir/us/davinci-pdex/index.html
https://github.com/Open-Health-Manager/standard-patient-health-record-ig
https://open-health-manager.github.io/standard-patient-health-record-ig/
https://confluence.hl7.org/display/PE/Patient+Empowerment+Home
https://confluence.hl7.org/display/PA


https://launch.smarthealthit.org/?auth_error=&fhir_version_2=r4&iss=&launch_pt=1&launch_url=&patient=&prov_skip_auth=1&provider=&pt_skip_auth=1&public_key=&sde=&token_lifetime=15&user_pt=


