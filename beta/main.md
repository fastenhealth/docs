---
layout: default
title: Setting up Fasten to Use With Real Medical Data
parent: Getting started
description: "Setting up Fasten to use with real medical data"
nav_order: 1
---

# Setting up Fasten to Use With Real Medical Data

This version allows you to connect to 650+ different Healthcare providers, using your existing accounts. It will allow you to connect and retrive your full electronic medical record and store it within Fasten.

Run the following commands to download and start the Fasten docker container.

```
docker pull ghcr.io/fastenhealth/fasten-onprem:main
docker run --rm -p 9090:8080 ghcr.io/fastenhealth/fasten-onprem:main
```

Next, open a browser to [http://localhost:9090](http://localhost:9090)

At this point you'll be redirected to the login page.

## Logging In

Once you've been redirected to the login page, you'll need to create an account at [http://localhost:9090/web/auth/signup](http://localhost:9090/web/auth/signup).

It can be as simple as

- **Username:** `testuser`
- **Password:** `testtest`

Congrats! You're now logged in. You'll be redirected to the dashboard, which will be empty until you connect a healthcare provider.

## Dashboard

Once you login, you'll be taken to the dashboard.
From here you can explore the data retrieved from the various healthcare providers.
This page will intially be empty, see the next section - `Connecting a new Source` - for more info.

## Connecting a new Source

Before you can use Fasten, you'll need to connect a healthcare provider.

If you're using the `main` flavor of Fasten, find a Source where you have an account, and login with your credentials.

Congrats, you're all set! Fasten will now start syncing your medical records.
