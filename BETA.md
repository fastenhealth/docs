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

Att his point you'll be redirected to the login page. 

### Logging In

The Fasten BETA contains a pre-populated database with a test user.
You can login to this test user with the following credentials:

**Username:** test@test.com
**Password:** testtest

### Dashboard

Once you login, you'll be taken to the dashboard. 
Now you can explore the data retrieved from the various healthcare providers.


### Connecting a new Source
You'll 

| Source | Credentials |
| --- | --- |
| Aetna | Username: `aetnaTestUser3` <br>Password: `FHIRdemo2020` |
| AthenaHealth | Username: `phrtest_preview@mailinator.com` <br>Password: `Password1` | 
| Medicare | Username: `BBUser00000` <br>Password: `PW00000!` |
| CareEvolution | Username: `CEPatient` <br>Password: `CEPatient2018` |
| Cerner | Username: `nancysmart` <br>Password: `Cerner01` |
| Cigna | Username: `syntheticuser05` <br>Password: `5ynthU5er5` |
| Epic | Username: `fhircamila` <br>Password: `epicepic1` |
| HealthIT | Username: `demouser` <br>Password: `Demouser1!` |
| Logica | Username: <br>Password: |
