---
layout: default
title: FAQs
---

> Most of these answers are copied responses to questions from Reddit:
> https://www.reddit.com/r/selfhosted/comments/xj9rx7/introducing_fasten_a_selfhosted_personal/

## What about HIPAA?

>[Health Insurance Portability and Accountability Act of 1996 (HIPAA)](https://aspe.hhs.gov/report/health-insurance-portability-and-accountability-act-1996), Public Law 104-191, included Administrative Simplification provisions that required HHS to adopt national standards for electronic health care transactions and code sets, unique health identifiers, and security. At the same time, Congress recognized that advances in electronic technology could erode the privacy of health information. Consequently, Congress incorporated into HIPAA provisions that mandated the adoption of Federal privacy protections for individually identifiable health information.
>
> https://www.hhs.gov/hipaa/for-professionals/index.html

Most of us are aware that HIPAA ensures that our medical data stays private and protected. However you may not be aware that HIPAA also guarantees Rights of Access to individuals. Basically you have access to your data, and you can do with it what you'd like. (Including storing it on your home server!)

> The Privacy Rule, a Federal law, gives you rights over your health information and sets rules and limits on who can look at and receive your health information. The Privacy Rule applies to all forms of individuals' protected health information, whether electronic, written, or oral. The Security Rule is a Federal law that requires security for health information in electronic form.

> See [lega/HIPAA.md](./legal/HIPAA.md) for more information. 

## Can I manually add my Medical data?

Fasten will support manual data entry, but I don't think it'll be a day-1 feature. It's a lot more complicated and the UI/UX will be pretty complicated.

At that point I'll probably need to hire a UX designer tbh.

## Where is my Medical data stored?

Fasten is self-hosted (you run it on your own hardware). I'll never have access to your medical data (it never transits a server under my control) - your medical data is directly transferred from the medical providers to your computer/server, so it's only stored on your hardware.


## How is my Medical data protected?

Fasten will definitely be storing its data encrypted at rest, however that functionality is not enabled yet.

I'm still debating the tradeoffs between whole-database encryption vs record encryption, as searchability is definitely something fasten users will want.

## Is my Medical data available offline if I'm unable to communciate with the Provider?
100%, the (raw) data is stored in a local SQLite DB, and the app will be designed so it can work offline (with certain functionality disabled -- like automatic updates).

## Will there be a cloud-based offering of Fasten?

I'm hesitant to go down the Cloud/SAAS model since Fasten would become a huge target, and would need to become HIPAA compliant.

I've been working on complaint software/infrastructure (PCI, HIPAA, SOC, FedRAMP) for most of my career and ideally I'd like to keep Fasten non-compliant -- with no access to medical/customer data.

1. TBH, if healthcare data was aggregated and managed by a single organization in the cloud, it would become a massive target and a likely source of data-breaches.
2. They would have to be HIPAA compliant. As someone who has developed complaint software -- HIPAA, SOC, PCI, FedRAMP -- for most of my career, I don't want to touch that ball of wax with Fasten.
3. Personally, I wouldn't trust a single company with all my healthcare data, especially a for-profit. I think many of us in [/r/selfhosted](https://www.reddit.com/r/selfhosted) feel the same way.

## What is the Fasten Lighthouse? I thought Fasten was Self-Hosted?


1. The Lighthouse allows users to search for any supported healthcare institution by name, tag, address (and eventually country). It returns logos and additional metadata about the endpoint so that the Fasten application knows how to correctly communicate with the healthcare institution. As you can imagine, this dataset will be large ([NPPES](https://www.cms.gov/Regulations-and-Guidance/Administrative-Simplification/NationalProvIdentStand/DataDissemination) is 8gb by itself -- and that only contains US institutions). 
2. Conforming US Healthcare institutions must allow patient access using the SMART-on-FHIR authentication protocol (its basically OpenID Connect). This means that app developers need to register an app with each EMR system (and sometimes each institution) and then securely store the returned client_id and client_secret. 
	- Registering applications is supposed to be simple, however in practice it can be a huge pain in the ass (legal contracts, privacy policies, technical documentation, audits, registered corporation, etc) -- its part of the reason why progress in [PLATFORM_LIST.md](https://github.com/fastenhealth/fasten-sources/blob/main/PLATFORM_LIST.md) is taking so long. I think that more PHR applications in the healthcare space will force EMR systems to streamline their developer onboarding flow, but until then a service like Fasten Lighthouse is required to have even a minimally functional user-experience. 
3. Fasten Lighthouse is designed such that it is only involved in the authentication flow, but it doesn't have access to the AccessToken/RefreshToken (by leveraging [PKCE](https://auth0.com/docs/get-started/authentication-and-authorization-flow/authorization-code-flow-with-proof-key-for-code-exchange-pkce)), and no patient data ever transits the service (the requests are made directly by the Fasten Go backend, running on your own hardware). See [FastenHealth/docs AUTHENTICATION.md](https://github.com/fastenhealth/docs/blob/main/technical/AUTHENTICATION.md) for more information and a data transfer diagram.

Regarding an "open source the Fasten Lighthouse" -- unfortunately for now the Fasten Lighthouse will remain closed source. 
- I'm still unsure about the Fasten monetization strategy (which will probably involve the Lighthouse since all new-connections require it)
- I do plan on releasing a "spec" for the Fasten Lighthouse API (other than search, its a pretty simple service under the hood)

## How do you plan on monetizing Fasten?

I think there's lots of possibilities for monetization, however I want to be thoughtful about it. 

Ideally Fasten will become a zero-knowledge application, where monetizing user-data is a non-starter. However there's a couple of different ways to still build a viable company, given that integrating with healthcare providers is so high-friction. 


- (SAAS) free open-source self-hosted version but charge for cloud-hosted version - this broadens our market to include non-technical users and allows for the possibility of sharing data with healthcare institutions (with the patients consent)
- (DATA-BROKER) become a data-platform/gateway, similar to plaid, and charge institutions to integrate with Fasten. This means when a patient changes healthcare providers/insurance companies, they may see an "import" button in their patient portals to pull their full history from Fasten into their provider. This is only viable if Fasten has significant market share. 
- (NICHE-GROWTH/REFERRALS) become a data-gateway, for a specific niche. Partner with researchers/providers that work with  high-risk groups (diabetics, liver disease, etc) and build dashboard widgets focused on providing relevant information for those patient types, so that the researchers and providers in that niche direct all new users towards Fasten. rinse-and-repeat for other diseases, then tackle Enterprise agreements. This strategy can also be used to offer condition/disease-specific referrals & services (Continuous-Glucose-Monitoring/home-care-monitoring) 


Ideally Fasten is free for self-hosted users, and free/minimal cost for cloud-users. Eventually I'd like to partner with (and charge) medical institutions, as B2B/B2E is the most lucrative, but it'll probably be a long time before that's viable. Personally I'm not depending on Fasten making money anytime soon, I just want to build something that will help people track their medical information, and build a community around it. If our community becomes big enough, monetization will be easy. The community will support the sharing features since they are in control, and our goals align.
