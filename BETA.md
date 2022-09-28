# Fasten BETA Instructions

Welcome to the Fasten Beta!

If you haven't already, please fill out this [Google Form](https://forms.gle/SNsYX9BNMXB6TuTw6)

## Getting Started

This Beta is provided with a couple of caveats:

- Fasten is still closed-source (please see the Reddit discussion for more info)
- The Beta version is only available as a Docker image (eventually we'll support other modes of distribution)
- Fasten is still a work-in-progress (many buttons in the UI do not do anything)
- Fasten can only connect to a handful of healthcare providers, but only their Sandbox accounts
	- Sandbox accounts are meant for testing, and contain synthetic(fake) data to give you an idea what Fasten will look like, without requiring personal medical information. 

## Instructions

Run the following commands to download and start the Fasten docker container.
```
docker pull ghcr.io/fastenhealth/fasten-onprem:sandbox 
docker run --rm -p 9090:8080 ghcr.io/fastenhealth/fasten-onprem:sandbox 
```

Next, open a browser to http://localhost:9090

At this point you'll be redirected to the login page. 

### Logging In

The Fasten BETA contains a pre-populated database with a test user.
You can login to this test user with the following credentials:

- **Username:** `test@test.com`
- **Password:** `testtest`

### Dashboard

Once you login, you'll be taken to the dashboard. 
From here you can explore the data retrieved from the various healthcare providers.


### Connecting a new Source
You may want to try (re)connecting a health care provider.
To do so, you'll need to use a Sandbox user and password from the table below.

> You should not (and cannot) use real credentials to test Fasten. 

| Source | Credentials | Link |
| --- | --- | ---  | 
| Aetna | Username: `aetnaTestUser3` <br>Password: `FHIRdemo2020` | |
| AthenaHealth | Username: `phrtest_preview@mailinator.com` <br>Password: `Password1` | [test accounts](https://docs.athenahealth.com/api/guides/onboarding-overview)
| Medicare | Username: `BBUser00000` <br>Password: `PW00000!` | [test accounts](https://bluebutton.cms.gov/developers/#developer-guidelines) |
| CareEvolution | Username: `CEPatient` <br>Password: `CEPatient2018` | [test accounts](https://fhir.careevolution.com/TestPatientAccounts.html) |
| Cerner | Username: `nancysmart` <br>Password: `Cerner01` | [test accounts](https://docs.google.com/document/d/10RnVyF1etl_17pyCyK96tyhUWRbrTyEcqpwzW-Z-Ybs/edit)|
| Cigna | Username: `syntheticuser05` <br>Password: `5ynthU5er5` | [test accounts](https://developer.cigna.com/service-apis/patient-access/sandbox#How-to-Use-the-Sandbox-Sandbox-Test-Users) |
| Epic | Username: `fhircamila` <br>Password: `epicepic1` | [test accounts](https://fhir.epic.com/Documentation?docId=testpatients)|
| HealthIT | Username: `demouser` <br>Password: `Demouser1!` | [test accounts](https://fhirsandbox.healthit.gov/secure/r4/view/userlogin.html)|
| Logica | Username: <br>Password: | |

Some providers (such as Cerner) may take a long time to sync, as their sandbox accounts have lots of test data. Please be patient. 

### Testing Manual Bundle Upload

If you'd like to test the manual bundle upload, you can use data provided by the [Synthea](https://synthetichealth.github.io/synthea-sample-data/downloads/synthea_sample_data_fhir_r4_sep2019.zip) project to test. 
Just extract the downloaded `zip` file, and upload one of the many `json`  files. 


## Feedback

If you notice any (non-obvious) issues with Fasten, please feel free to open an issue on Github. 
If you have any ideas or feedback for how to make Fasten better, please also consider opening an issue on Github. 

https://github.com/fastenhealth/docs/issues

### Discord
Please consider joining the Fasten Discord as well. I'll be keeping an eye on it, and answering questions. 

https://discord.gg/2bEy6Y2d

