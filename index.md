---
layout: default
title: Welcome
description: "What is Fasten?"
nav_order: 0
---

# What is Fasten?

{: .fs-6 .fw-300 }
Fasten is an open-source and self-hosted electronic medical record aggregator for individuals and families. Securely connect your healthcare providers together, creating a personal health record that never leaves your hands.

[Get started now](/getting-started/){: .btn .btn-primary .fs-5 .mb-4 .mb-md-0 .mr-2 }
[View on GitHub](https://github.com/fastenhealth/fasten-onprem/){: .btn .fs-5 .mb-4 .mb-md-0 }

---

{: .warning }

> Fasten is a Work-in-Progress and can only communicate with a limited number of Healthcare Instutions (approx 25,000 at last count).
> Please fill out this [Google Form](https://forms.gle/SNsYX9BNMXB6TuTw6) if you'd like to be kept up-to-date on Fasten
>
> To ensure Fasten's long-term sustainability, we're exploring some funding options. While we're still deciding a long-term monetization strategy, I'm kicking off with a crowdfunding/fundraising experiment for the first 500 users (including a surprise desktop app):
>
> - [Fasten Self-Hosted Lifetime License - **$200**](https://buy.stripe.com/fZe00deiUexS58Y4gg)
>
> Got questions or want to learn more about our fundraising experiment? [Click here to dive into the details & FAQs](https://docs.fastenhealth.com/FUNDRAISING.html)

# Introduction

Like many of you, I've worked for many companies over my career. In that time, I've had multiple health, vision and dental
insurance providers, and visited many different clinics, hospitals and labs to get procedures & tests done.

Recently I had a semi-serious medical issue, and I realized that my medical history (and the medical history of my family members)
is a lot more complicated than I realized and distributed across the many healthcare providers I've used over the years.
I wanted a single (private) location to store our medical records, and I just couldn't find any software that worked as I'd like:

- **Self-hosted** - this is my medical history, I'm not willing to give it to some random multi-national corporation to data-mine and sell
- **All inclusive** - It should aggregate my data from multiple healthcare providers (insurance companies, hospital networks, clinics, labs) across multiple industries (vision, dental, medical) -- all in one dashboard
- **Automatic** - It should pull my EMR (electronic medical record) directly from my insurance provider/clinic/hospital network - I dont want to scan/OCR physical documents (unless I have to)
- **Open Source** - The code should be available for contributions & auditing

So, I built it.

**Fasten is an open-source, self-hosted, personal/family electronic medical record aggregator, designed to integrate with 100,000's of insurances/hospitals/clinics**

<p align="center">
  <a href="https://imgur.com/a/vfgojBD">
  <img alt="fasten_view" src="https://i.imgur.com/UaZyEbN.png">
  </a>
  <br/>
  <a href="https://imgur.com/a/vfgojBD">See more Fasten screenshots</a>
</p>

# Features

Fasten is designed with a solid foundation that is easily extensible:

- Self-hosted
- Designed for families, not Clinics (unlike OpenEMR and other popular EMR systems)
- Supports the Medical industry's (semi-standard) FHIR protocol
- Uses OAuth2 (Smart-on-FHIR) authentication (no passwords necessary)
- Uses OAuth's `offline_access` scope (where possible) to automatically pull changes/updates
- Multi-user support for household/family use
- (Future) Dashboards & tracking for diagnostic tests
- (Future) Integration with smart-devices & wearables

---

See [FAQs](./FAQs.md) for common questions (& answers) regarding Fasten

See [FEATURES](./FEATURES.md) for a list of features that are planned for Fasten
