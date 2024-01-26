---
layout: default
title: Setting up Fasten to Use Fake Test Data
parent: Getting started
description: "Setting up Fasten to use fake test data"
nav_order: 2
---

# Setting up Fasten to Use Fake Test Data

{: .warning }

> The instructions below are for the `sandbox` flavor of Fasten, which cannot connect to real patient portals. If you'd like to use Fasten with your real healthcare accounts, please follow the instructions [here](/getting-started/main.html).

These instructions will help you set up a version of Fasten that only allows you to connect to a handful of Healthcare providers using Sandbox accounts that are meant for testing and contain synthetic(fake) data to give you an idea of what Fasten will look like without requiring personal medical information.

Run the following commands to download and start the Fasten docker container.

```
docker pull ghcr.io/fastenhealth/fasten-onprem:main

docker run --rm \
-p 9090:8080 \
-v `pwd`/db:/opt/fasten/db \
-v `pwd`/cache:/opt/fasten/cache \
ghcr.io/fastenhealth/fasten-onprem:sandbox

```

Next, open a browser to [http://localhost:9090](http://localhost:9090)

At this point, you'll be redirected to the login page.

## Logging In

Once you've been redirected to the login page, you'll need to create an account at [http://localhost:9090/web/auth/signup](http://localhost:9090/web/auth/signup).

Provide your name, a username, and a password and click `Create Account`.

You should now be now logged in. You'll be redirected to the dashboard, which will be empty until you connect with a healthcare provider.

## Dashboard

Once you login, you'll be taken to the dashboard.
From here, you can explore the data retrieved from the various healthcare providers.
This page will initially be empty; see the next section - `Connecting a new Source` - for more info.

## Connecting a new Source

Before you can use Fasten, you'll need to connect a healthcare provider.

This version only allows you to connect to a handful of Healthcare providers using Sandbox accounts that are meant for testing and contain synthetic(fake) data to give you an idea of what Fasten will look like without requiring personal medical information.

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

Some providers (such as Cerner) may take a long time to sync as their sandbox accounts have lots of test data. Please be patient.

## Testing Manual Bundle Upload

If you'd like to test the manual bundle upload, you can use data provided by the [Synthea](https://synthetichealth.github.io/synthea-sample-data/downloads/synthea_sample_data_fhir_r4_sep2019.zip) project to test.
Just extract the downloaded `zip` file and upload one of the many `json` files.
