---
layout: default
title: Fasten BETA Instructions
---

# Fasten BETA Instructions

Welcome to the Fasten Beta!

If you haven't already, please fill out this [Google Form](https://forms.gle/SNsYX9BNMXB6TuTw6)

## Getting Started

This Beta is provided with a couple of caveats:

- Fasten is still partially closed-source (please see the Reddit discussion for more info)
- The Beta version is only available as a Docker image (eventually we'll support other modes of distribution)
- Fasten is still a work-in-progress (many buttons in the UI do not do anything)

## Instructions

There are 2 flavors of Fasten:
- `sandbox` - This version only allows you to connect to a handful of Healthcare providers, using Sandbox accounts that are meant for testing, and contain synthetic(fake) data to give you an idea what Fasten will look like, without requiring personal medical information.
- `main` - This version allows you to connect to 650+ different Healthcare providers, using your existing accounts. It will allow you to connect and retrive your full electronic medical record and store it within Fasten. 

Run the following commands to download and start the Fasten docker container.

> The instructions below are for the `sandbox` flavor of Fasten. If you'd like to connect using your real account, please use `ghcr.io/fastenhealth/fasten-onprem:main` in the commands below.

```
docker pull ghcr.io/fastenhealth/fasten-onprem:sandbox 
docker run --rm -p 9090:8080 ghcr.io/fastenhealth/fasten-onprem:sandbox 
```


Next, open a browser to http://localhost:9090

At this point you'll be redirected to the login page. 

### Logging In

Before you can use the Fasten BETA you'll need to [Create an Account](http://localhost:9090/web/auth/signup).

It can be as simple as
- **Username:** `testuser`
- **Password:** `testtest`

> See `Connecting a new Source` below for credentials you can use to connect to healthcare providers. 

### Dashboard

Once you login, you'll be taken to the dashboard. 
From here you can explore the data retrieved from the various healthcare providers.
This page will intially be empty, see the next section - `Connecting a new Source`  - for more info.


### Connecting a new Source
Before you can use Fasten, you'll need to connect a healthcare provider.

#### Production (Main) Flavor

If you're using the `main` flavor of Fasten, find a Source where you have an account, and login with your credentials. 

#### Sandbox Flavor

This version only allows you to connect to a handful of Healthcare providers, using Sandbox accounts that are meant for testing, and contain synthetic(fake) data to give you an idea what Fasten will look like, without requiring personal medical information.

To do so, you'll need to use a Sandbox user and password from the table below. You should not (and cannot) use real credentials with the Sandbox version of Fasten. 

| Source | Credentials | Link |
| --- | --- | ---  | 
| Aetna | Username: `aetnaTestUser3` <br>Password: `FHIRdemo2020` | |
| AllScripts | Username: `alice.newman@sunrise184region.com` <br>Password: `Allscripts#1` | [test accounts](https://developer.allscripts.com/Content/fhir/FHIRSandboxes_index.html)
| AthenaHealth | Username: `phrtest_preview@mailinator.com` <br>Password: `Password1` | [test accounts](https://docs.athenahealth.com/api/guides/onboarding-overview)
| CareEvolution | Username: `CEPatient` <br>Password: `CEPatient2018` | [test accounts](https://fhir.careevolution.com/TestPatientAccounts.html) |
| Cerner | Username: `nancysmart` <br>Password: `Cerner01` | [test accounts](https://docs.google.com/document/d/10RnVyF1etl_17pyCyK96tyhUWRbrTyEcqpwzW-Z-Ybs/edit)|
| Cigna | Username: `syntheticuser05` <br>Password: `5ynthU5er5` | [test accounts](https://developer.cigna.com/service-apis/patient-access/sandbox#How-to-Use-the-Sandbox-Sandbox-Test-Users) |
| eClinicalWorks/Healow | Username: `AdultFemaleFHIR` <br>Password: `e@CWFHIR1` | [test accounts](https://fhir.eclinicalworks.com/ecwopendev/)|
| Epic | Username: `fhircamila` <br>Password: `epicepic1` | [test accounts](https://fhir.epic.com/Documentation?docId=testpatients)|
| HealthIT | Username: `demouser` <br>Password: `Demouser1!` | [test accounts](https://fhirsandbox.healthit.gov/secure/r4/view/userlogin.html)|
| Kaiser | Username: <br>Password: | |
| Logica | Username: <br>Password: | |
| Medicare | Username: `BBUser00000` <br>Password: `PW00000!` | [test accounts](https://bluebutton.cms.gov/developers/#developer-guidelines) |
| Meditech | Username: <br>Password: | |
| NextGen | Username: <br>Password: | |

Some providers (such as Cerner) may take a long time to sync, as their sandbox accounts have lots of test data. Please be patient. 

### Testing Manual Bundle Upload



If you'd like to test the manual bundle upload, you can use data provided by the [Synthea](https://synthetichealth.github.io/synthea-sample-data/downloads/synthea_sample_data_fhir_r4_sep2019.zip) project to test. 
Just extract the downloaded `zip` file, and upload one of the many `json`  files. 


## Feedback

If you notice any (non-obvious) issues with Fasten, please feel free to open an issue on Github. 
If you have any ideas or feedback for how to make Fasten better, please also consider opening an issue on Github. 

https://github.com/fastenhealth/docs/issues

### Discord
Please consider joining the Fasten Discord as well. I'll be keeping an eye on it, and answering questions as they come up.

https://discord.gg/Bykz6BAN8p


