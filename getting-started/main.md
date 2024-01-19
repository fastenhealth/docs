---
layout: default
title: Setting up Fasten to Use With Real Medical Data
parent: Getting started
description: "Setting up Fasten to use with real medical data"
nav_order: 1
---

# Setting up Fasten to Use With Real Medical Data

These instructions will help you set up a version of Fasten that lets you connect to 27,000+ institutions using your existing accounts. It will enable you to connect and retrieve your full electronic medical record and store it within Fasten.

Run the following commands to download and start the Fasten docker container.

```
docker pull ghcr.io/fastenhealth/fasten-onprem:main

docker run --rm \
-p 9090:8080 \
-v `pwd`/db:/opt/fasten/db \
-v `pwd`/cache:/opt/fasten/cache \
ghcr.io/fastenhealth/fasten-onprem:main

```

To see if Fasten is running, open [http://localhost:9090](http://localhost:9090) in your browser.

Congrats, you've successfully started Fasten!

## Logging In

Once Fasten has started, you'll next need to create an account by clicking the [Create an Account button](http://localhost:9090/web/auth/signup) on the login screen. You'll be prompted to enter your name, a username, and a password.

Provide your name, a username, and a password and click `Create Account`.

You should now be now logged in. You'll be redirected to the dashboard, which will be empty until you connect with a healthcare provider.

## Dashboard

Once you log in, you'll be taken to the dashboard.
From here, you can explore the data retrieved from the various healthcare providers.
This page will initially be empty; see the next section - `Connecting a new Source` - for more info.

## Connecting a new Source

Before you can use Fasten, you'll need to connect a healthcare provider.

Click the `Add Source` button, scroll down to the `HEALTHCARE COMPANIES` section, and search for a patient portal to connect. Once you've selected a portal, follow the prompts and log in with your patient portal credentials. Once you've logged in, you'll be redirected back to the dashboard. Please note that syncing your medical records can take a while, so please be patient.

Congrats, you're all set! Fasten will now start syncing your medical records.
