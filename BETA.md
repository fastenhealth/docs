---
layout: default
title: Getting started
description: "Getting started with self-hosting the Fasten Beta"
nav_order: 1
---

# Welcome to the Fasten Beta

Welcome to the Fasten beta! This beta is provided with a couple of caveats:

- Fasten is still partially closed-source (please see the Reddit discussion for more info)
- The Beta version is only available as a Docker image (eventually we'll support other modes of distribution)
- Fasten is still a work-in-progress (many buttons in the UI do not do anything)

If you haven't already, please fill out this [Google Form](https://forms.gle/SNsYX9BNMXB6TuTw6)

## Getting Started

Below are instructions to get started with self hosting the Fasten Beta.

Fasten comes in two flavors depending on whether you want to use it with your real medical records, or just test it out with fake data.

{: .fs-6 .fw-300 }

How would you like to use Fasten?

[With real medical records](#setting-up-fasten-to-use-with-real-medical-data){: .btn .btn-primary .fs-5 .mb-4 .mb-md-0 .mr-2 }
[With fake test data](#setting-up-fasten-to-use-fake-test-data-sandbox){: .btn .fs-5 .mb-4 .mb-md-0 }

---

### Setting up Fasten to use with real medical data

This version allows you to connect to 650+ different Healthcare providers, using your existing accounts. It will allow you to connect and retrive your full electronic medical record and store it within Fasten.

Run the following commands to download and start the Fasten docker container.

```
docker pull ghcr.io/fastenhealth/fasten-onprem:main
docker run --rm -p 9090:8080 ghcr.io/fastenhealth/fasten-onprem:main
```

Next, open a browser to [http://localhost:9090](http://localhost:9090)

At this point you'll be redirected to the login page.

#### Logging In

Once you've been redirected to the login page, you'll need to create an account at [http://localhost:9090/web/auth/signup](http://localhost:9090/web/auth/signup).

It can be as simple as

- **Username:** `testuser`
- **Password:** `testtest`

Congrats! You're now logged in. You'll be redirected to the dashboard, which will be empty until you connect a healthcare provider.

#### Dashboard

Once you login, you'll be taken to the dashboard.
From here you can explore the data retrieved from the various healthcare providers.
This page will intially be empty, see the next section - `Connecting a new Source` - for more info.

#### Connecting a new Source

Before you can use Fasten, you'll need to connect a healthcare provider.

If you're using the `main` flavor of Fasten, find a Source where you have an account, and login with your credentials.

Congrats, you're all set! Fasten will now start syncing your medical records.

---

### Setting up Fasten to use fake test data (Sandbox)

{: .warning }

> The instructions below are for the `sandbox` flavor of Fasten, which cannot connect to real patient portals. If you'd like to use Fasten with your real healthcare accounts, please follow the instructions [here](#setting-up-fasten-main).

This version only allows you to connect to a handful of Healthcare providers, using Sandbox accounts that are meant for testing, and contain synthetic(fake) data to give you an idea what Fasten will look like, without requiring personal medical information.

Run the following commands to download and start the Fasten docker container.

Next, open a browser to [http://localhost:9090](http://localhost:9090)

At this point you'll be redirected to the login page.

#### Logging In

Once you've been redirected to the login page, you'll need to create an account at [http://localhost:9090/web/auth/signup](http://localhost:9090/web/auth/signup).

It can be as simple as

- **Username:** `testuser`
- **Password:** `testtest`

Congrats! You're now logged in. You'll be redirected to the dashboard, which will be empty until you connect a healthcare provider.

#### Dashboard

Once you login, you'll be taken to the dashboard.
From here you can explore the data retrieved from the various healthcare providers.
This page will intially be empty, see the next section - `Connecting a new Source` - for more info.

#### Connecting a new Source

Before you can use Fasten, you'll need to connect a healthcare provider.

This version only allows you to connect to a handful of Healthcare providers, using Sandbox accounts that are meant for testing, and contain synthetic(fake) data to give you an idea what Fasten will look like, without requiring personal medical information.

To do so, you'll need to use a Sandbox user and password from the table below. You should not (and cannot) use real credentials with the Sandbox version of Fasten.

| Source                | Credentials                                                                | Link                                                                                                                                  |
| --------------------- | -------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------- |
| Aetna                 | Username: `aetnaTestUser3` <br>Password: `FHIRdemo2020`                    |                                                                                                                                       |
| AllScripts            | Username: `alice.newman@sunrise184region.com` <br>Password: `Allscripts#1` | [test accounts](https://developer.allscripts.com/Content/fhir/FHIRSandboxes_index.html)                                               |
| AthenaHealth          | Username: `phrtest_preview@mailinator.com` <br>Password: `Password1`       | [test accounts](https://docs.athenahealth.com/api/guides/onboarding-overview)                                                         |
| CareEvolution         | Username: `CEPatient` <br>Password: `CEPatient2018`                        | [test accounts](https://fhir.careevolution.com/TestPatientAccounts.html)                                                              |
| Cerner                | Username: `nancysmart` <br>Password: `Cerner01`                            | [test accounts](https://docs.google.com/document/d/10RnVyF1etl_17pyCyK96tyhUWRbrTyEcqpwzW-Z-Ybs/edit)                                 |
| Cigna                 | Username: `syntheticuser05` <br>Password: `5ynthU5er5`                     | [test accounts](https://developer.cigna.com/service-apis/patient-access/sandbox#How-to-Use-the-Sandbox-Sandbox-Test-Users)            |
| eClinicalWorks/Healow | Username: `AdultFemaleFHIR` <br>Password: `e@CWFHIR1`                      | [test accounts](https://fhir.eclinicalworks.com/ecwopendev/)                                                                          |
| Epic                  | Username: `fhircamila` <br>Password: `epicepic1`                           | [test accounts](https://fhir.epic.com/Documentation?docId=testpatients)                                                               |
| HealthIT              | Username: `demouser` <br>Password: `Demouser1!`                            | [test accounts](https://fhirsandbox.healthit.gov/secure/r4/view/userlogin.html)                                                       |
| Kaiser                | Username: <br>Password:                                                    |                                                                                                                                       |
| Logica                | Username: <br>Password:                                                    |                                                                                                                                       |
| Medicare              | Username: `BBUser00000` <br>Password: `PW00000!`                           | [test accounts](https://bluebutton.cms.gov/developers/#developer-guidelines)                                                          |
| Meditech              | Username: <br>Password:                                                    |                                                                                                                                       |
| NextGen               | Username: `patientapitest` <br>Password: `Password1!`                      | [test accounts](https://www.nextgen.com/-/media/files/api/nge-patient-api-auth-guide.pdf)                                             |
| VA Health             | Username: `va.api.user+idme.101@gmail.com` <br>Password: `Password1234!`   | [test accounts](https://github.com/department-of-veterans-affairs/vets-api-clients/blob/master/test_accounts/health_test_accounts.md) |

Some providers (such as Cerner) may take a long time to sync, as their sandbox accounts have lots of test data. Please be patient.

#### Testing Manual Bundle Upload

If you'd like to test the manual bundle upload, you can use data provided by the [Synthea](https://synthetichealth.github.io/synthea-sample-data/downloads/synthea_sample_data_fhir_r4_sep2019.zip) project to test.
Just extract the downloaded `zip` file, and upload one of the many `json` files.

---

## Feedback

If you notice any (non-obvious) issues with Fasten, please feel free to [open an issue on Github](https://github.com/fastenhealth/docs/issues).
If you have any ideas or feedback for how to make Fasten better, please also consider [opening an issue on Github](https://github.com/fastenhealth/docs/issues).

### Discord

Please consider joining the [Fasten Discord](https://discord.gg/Bykz6BAN8p) as well. I'll be keeping an eye on it, and answering questions as they come up.
