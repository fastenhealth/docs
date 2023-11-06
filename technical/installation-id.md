---
title: Installation ID
parent: Technical
---

While Fasten has been able to integrate with 27,000+ health care institutions, some of the 
largest institutions are pushing back because they have concerns about the potential for abuse 
given the way the Fasten Lighthouse works.

> Just a refresher, Fasten Lighthouse is an auth gateway, providing a publicly accessible server for the provider to 
> redirect the user to (with their OAuth code) after authentication. Fasten Lighthouse then redirects the user to their 
> local/localhost installation of Fasten where the code is swapped for an Access Token. (In some cases the Fasten 
> Lighthouse may also be involved in the OAuth code-> access token swap) 
> 
> See: https://github.com/fastenhealth/docs/blob/main/technical/authentication.md


Here are their concerns in a nutshell:
- Fasten Lighthouse is a completely stateless application
- Theres no way to determine how many users are associated with the same Fasten installation (container/desktop app)
    - **FEAR**: a Fasten self-hoster may offer their server publicly, providing  access to a large number of users  without 
      having to agree to or follow the privacy policy and terms of use that I shared with the provider to get API credentials.
- Fasten Lighthouse doesn’t(cant?) do any validation that it’s redirecting to an “official” Fasten application
    - **FEAR**: a completely separate application could use Fasten Lighthouse with their app, completely ignoring the audit 
      and security review process that the Provider has in place for vetting new applications.

Both of these concerns are completely valid, given the 10’s of millions of healthcare records some of these Healthcare providers protect.

---

After discussing potential solutions with the Providers, here’s what the community has agreed to:

- Fasten Self-Hosted will implement an installation ID mechanism, which would be sent along with every request to the Fasten Lighthouse. 
    The Installation ID will be associated with a Fasten Self-Hosted administrator Name + Email address (for contact purposes).
- Fasten Lighthouse will enforce Provider limits for # of registered users per installation ID — in the order of XX rather than XXX
    (so 10s of users rather than 100’s of users)
- The idea is that if each installation of Fasten Self-Hosted is limited to XX users per Provider, then the fallout of a
    misconfiguration or malicious application is limited.
- You would only need to register an Installation ID once, and it would basically be another config file. The registration 
    information (Name + Email) would only be used to notify system admins if they’re reaching a user limit for a specific Provider.
- Fasten Lighthouse is **NOT** involved in requesting your medical records from your Provider (that communication is always
    done directly between your Fasten self-hosted instance and the Provider -- this does not change with this proposal -- only the Auth flow is modified)

---

Obviously this is non-optimal, but the potential for abuse with Lighthouse is a fact that’s come up numerous times with 
large Providers. None of these providers have ever seen an open-source application like Fasten before, so they're being 
extra cautious to make sure they're not missing anything.

---

# FAQ's

## Why do I need the Fasten Lighthouse? Can I create my own version of Fasten Lighthouse?

The Fasten Lighthouse is a required component of the Fasten system. It's the only way to get your medical records from your Provider.
Fasten Lighthouse is closed source, but it's fairly simple to run & I do plan on open-sourcing the API spec.
However, keep in mind that it's probably going to be difficult for an individual to recreate their own personal "Fasten Lighthouse"

- See [What is the Fasten Lighthouse? I thought Fasten was Self-Hosted?](../faqs.md#lighthouse)

## What if I don't want to register an Installation ID?

If you're only using Fasten to manually upload your records, you don't really need an Installation ID, since you won't be communicating with the Lighthouse at all. 

## Are you passing Installation ID's to the Provider?

No, the Installation ID is only used by the Fasten Lighthouse to enforce user limits -- it's a correlation ID. 
It's not passed to the Provider at all.

## What will be the "hard registration limit" per Installation ID?

That's still under discussion. It may end up being Provider specific, but I'm hoping that they'll agree to a reasonable constant limit ~100.

## Would User level encryption or Zero-Knowledge Encryption  help?

- **User level encryption** still requires the user to trust of the application. It won't protect users from a malicious app or
    malicious system admin, it only makes it more difficult/appealing for hackers who've found a way to dump the database.
- **[Zero-Knowledge Encryption](https://github.com/fastenhealth/docs/issues/57)** is a great idea, but it's not something that I can implement in the short term as it's complicated for a couple of reasons. 
    Medical record data is retrieved from the healthcare provider server-side (because a number of EHR systems don't support CORS in any 
    meaningful way, and server-side sync is basically required for background processing), so a malicious version of the 
    Fasten App could just dump it to a file that the malicious admin can see. Zero-knowledge encryption also doesn't solve the problem of a
    non-official Fasten app using the Fasten Lighthouse to skirt the Provider's security review process.

## Is it possible to have Providers redirect directly to the Fasten App, ignoring the Lighthouse completely? 

Unfortunately not. See [What is the Fasten Lighthouse? I thought Fasten was Self-Hosted?](../faqs.md#lighthouse) and [Authentication](authentication.md)

## Would Dynamic Client Registration help?

While [OAuth Dynamic Client Registration (DCR)](https://curity.io/resources/learn/openid-connect-understanding-dcr/) is a thing,
most Providers don't support it, and these big Providers that have legal and security compliance checklists before providing API credentials definitely don't. 

