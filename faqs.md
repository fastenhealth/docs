---
layout: default
title: FAQs
redirect_from:
- /FAQs.html
---

> Most of these answers are copied responses to questions from Reddit:
> https://www.reddit.com/r/selfhosted/comments/xj9rx7/introducing_fasten_a_selfhosted_personal/

## What about HIPAA?

>[Health Insurance Portability and Accountability Act of 1996 (HIPAA)](https://aspe.hhs.gov/report/health-insurance-portability-and-accountability-act-1996), Public Law 104-191, included Administrative Simplification provisions that required HHS to adopt national standards for electronic health care transactions and code sets, unique health identifiers, and security. At the same time, Congress recognized that advances in electronic technology could erode the privacy of health information. Consequently, Congress incorporated into HIPAA provisions that mandated the adoption of Federal privacy protections for individually identifiable health information.
>
> https://www.hhs.gov/hipaa/for-professionals/index.html

Most of us are aware that HIPAA ensures that our medical data stays private and protected. However you may not be aware that HIPAA also guarantees Rights of Access to individuals. Basically you have access to your data, and you can do with it what you'd like. (Including storing it on your home server!)

> The Privacy Rule, a Federal law, gives you rights over your health information and sets rules and limits on who can look at and receive your health information. The Privacy Rule applies to all forms of individuals' protected health information, whether electronic, written, or oral. The Security Rule is a Federal law that requires security for health information in electronic form.

> See [lega/HIPAA.md](./legal/hipaa.html) for more information. 

## Can I manually add my medical data?

Yes, Fasten presently supports adding medical data manually. To add medical data, you need to either create an encounter or append it to an existing encounter. This limitation may be removed in the future.

## Where is my Medical data stored?

Fasten is self-hosted (you run it on your own hardware). I'll never have access to your medical data (it never transits a server under my control) - your medical data is directly transferred from the medical providers to your computer/server, so it's only stored on your hardware.


## How is my Medical data protected?

Fasten supports [full database encryption](https://en.wikipedia.org/wiki/Database_encryption) to protect your data-at-rest, however users are responsible for [protecting their physical devices](https://www.okta.com/blog/2020/09/6-steps-to-practice-strong-laptop-security/).

As an additional layer of protection, we're considering record-level encryption, however that has some ramifications for search-ability.

## Is my Medical data available offline if I'm unable to communicate with the Provider?

100%, the (raw) data is stored in a local SQLite DB, and the app will be designed so it can work offline (with certain functionality disabled -- like automatic updates).

## Will there be a cloud-based offering of Fasten?

I'm hesitant to go down the Cloud/SAAS model since Fasten would become a huge target, and would need to become HIPAA compliant.

I've been working on complaint software/infrastructure (PCI, HIPAA, SOC, FedRAMP) for most of my career and ideally I'd like to keep Fasten non-compliant -- with no access to medical/customer data.

1. TBH, if healthcare data was aggregated and managed by a single organization in the cloud, it would become a massive target and a likely source of data-breaches.
2. They would have to be HIPAA compliant. As someone who has developed complaint software -- HIPAA, SOC, PCI, FedRAMP -- for most of my career, I don't want to touch that ball of wax with Fasten.
3. Personally, I wouldn't trust a single company with all my healthcare data, especially a for-profit. I think many of us in [/r/selfhosted](https://www.reddit.com/r/selfhosted) feel the same way.

## Does Fasten pull my records from a Health Information Exchange (HIE/HIX)

HIE's are ubiquitous and ONC's information blocking rules require providers to contribute PHI data for all patients to HIE's. However, HIE's have no way to determine which providers should have access to an individual's medical records, so they have no authorization layer preventing unauthorized access. Any healthcare employee authorized to access patient records through an HIE essentially has access to the medical records of everyone in the US.

**Fasten doesn't integrate with HIE/HIXs** and you will still be able to access your records, even if you decide to opt-out of HIE sharing. Fasten integrates directly with your healthcare institutions to retrieve your health records -- it's more tedious, but there's no middleman.

## What is the Fasten Lighthouse? I thought Fasten was Self-Hosted?
<a id="lighthouse"></a>

1. The Lighthouse allows users to search for any supported healthcare institution by name, tag, address (and eventually country). It returns logos and additional metadata about the endpoint so that the Fasten application knows how to correctly communicate with the healthcare institution. As you can imagine, this dataset will be large ([NPPES](https://www.cms.gov/Regulations-and-Guidance/Administrative-Simplification/NationalProvIdentStand/DataDissemination) is 8GB by itself -- and that only contains US institutions). 
2. Conforming US Healthcare institutions must allow patient access using the SMART-on-FHIR authentication protocol (its basically OpenID Connect). This means that app developers need to register an app with each EMR system (and sometimes each institution) and then securely store the returned client_id and client_secret. 
	- Registering applications is supposed to be simple, however in practice it can be a huge pain in the ass (legal contracts, privacy policies, technical documentation, audits, registered corporation, etc) -- its part of the reason why progress in [PLATFORM_LIST.md](https://github.com/fastenhealth/fasten-sources/blob/main/PLATFORM_LIST.md) is taking so long. I think that more PHR applications in the healthcare space will force EMR systems to streamline their developer onboarding flow, but until then a service like Fasten Lighthouse is required to have even a minimally functional user-experience. 
3. Fasten Lighthouse is designed such that it is only involved in the authentication flow. Where possible we leverage [PKCE](https://auth0.com/docs/get-started/authentication-and-authorization-flow/authorization-code-flow-with-proof-key-for-code-exchange-pkce) & Public Clients to ensure it does not have access to the Access Token & Refresh Token. 
	- In some cases, Healthcare providers will require a [Confidential client](https://oauth.net/2/client-types/), which means that the client application cannot directly exchange the authorization code for an access token, a Client Secret is necessary. For security purposes the Client Secret is not stored in the client application, but is stored on the Lighthouse server.
	- Confidential client token exchange requests must be proxied through the Lighthouse server (which is different from the Public Client flow), and will have temporary access to the Access Token. 
4. Patient data never transits the Fasten Lighthouse (the requests are made directly by the Fasten application, running on your own hardware). 
	- See [FastenHealth/docs AUTHENTICATION.md](https://github.com/fastenhealth/docs/blob/main/technical/authentication.html) for more information and a data transfer diagram.

Regarding an "open source the Fasten Lighthouse" -- unfortunately for now the Fasten Lighthouse will remain closed source. 
- I'm still unsure about the Fasten monetization strategy (which will probably involve the Lighthouse since all new-connections require it)
- I do plan on releasing a "spec" for the Fasten Lighthouse API (other than search, its a pretty simple service under the hood)

## How do you plan on monetizing Fasten?

I think there's lots of possibilities for monetization, however I want to be thoughtful about it. 

Ideally Fasten will become a zero-knowledge application, where monetizing user-data is a non-starter. However there's a couple of different ways to still build a viable company, given that integrating with healthcare providers is so high-friction. 


- (**SAAS/APP STORE**) free open-source self-hosted version but charge for cloud-hosted and app store versions - this broadens our market to include non-technical users and allows for the possibility of sharing data with healthcare institutions (with the patients consent)
- (**DATA-PLATFORM**) become a data-platform/gateway, similar to plaid, and charge institutions to integrate with Fasten. This means when a patient changes healthcare providers/insurance companies, they may see an "import" button in their patient portals to pull their full history from Fasten into their provider. This is only viable if Fasten has significant market share. 
- (**NICHE-GROWTH/REFERRALS**) become a data-gateway, for a specific niche. Partner with researchers/providers that work with  high-risk groups (diabetics, liver disease, etc) and build dashboard widgets focused on providing relevant information for those patient types, so that the researchers and providers in that niche direct all new users towards Fasten. Rinse-and-repeat for other diseases, then tackle enterprise agreements. This strategy can also be used to offer condition/disease-specific referrals & services (Continuous-Glucose-Monitoring/home-care-monitoring) 


Ideally Fasten is free for self-hosted users, and free/minimal cost for cloud-users. Eventually I'd like to partner with (and charge) medical institutions, as B2B/B2E is the most lucrative, but it'll probably be a long time before that's viable. Personally I'm not depending on Fasten making money anytime soon, I just want to build something that will help people track their medical information, and build a community around it. If our community becomes big enough, monetization will be easy. The community will support the sharing features since they are in control, and our goals align.
