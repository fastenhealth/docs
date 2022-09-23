> Most of these answers are copied responses to questions from Reddit:
> https://www.reddit.com/r/selfhosted/comments/xj9rx7/introducing_fasten_a_selfhosted_personal/

## What about HIPAA?

>[Health Insurance Portability and Accountability Act of 1996 (HIPAA)](https://aspe.hhs.gov/report/health-insurance-portability-and-accountability-act-1996), Public Law 104-191, included Administrative Simplification provisions that required HHS to adopt national standards for electronic health care transactions and code sets, unique health identifiers, and security. At the same time, Congress recognized that advances in electronic technology could erode the privacy of health information. Consequently, Congress incorporated into HIPAA provisions that mandated the adoption of Federal privacy protections for individually identifiable health information.
>
> https://www.hhs.gov/hipaa/for-professionals/index.html

Most of us are aware that HIPAA ensures that our medical data stays private and protected. However you may not be aware that HIPAA also guarantees Rights of Access to individuals. Basically you have access to your data, and you can do with it what you'd like. (Including storing it on your home server!)

> The Privacy Rule, a Federal law, gives you rights over your health information and sets rules and limits on who can look at and receive your health information. The Privacy Rule applies to all forms of individuals' protected health information, whether electronic, written, or oral. The Security Rule is a Federal law that requires security for health information in electronic form.


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

I'm hesitant to go down the Cloud/SAAS model since Fasten would have to become HIPAA compliant.

I've been working on complaint software/infrastructure (PCI, HIPAA, SOC, FedRAMP) for most of my career and ideally I'd like to keep Fasten non-compliant -- with no access to medical/customer data.

1. TBH, if healthcare data was aggregated and managed by a single organization in the cloud, it would become a massive target and a likely source of data-breaches.
2. They would have to be HIPAA compliant. As someone who has developed complaint software -- HIPAA, SOC, PCI, FedRAMP -- for most of my career, I don't want to touch that ball of wax with Fasten.
3. Personally, I wouldn't trust a single company with all my healthcare data, especially a for-profit. I think many of us in [/r/selfhosted](https://www.reddit.com/r/selfhosted) feel the same way.
