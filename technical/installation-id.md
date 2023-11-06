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
> See: https://docs.fastenhealth.com/faqs.html#what-is-the-fasten-lighthouse-i-thought-fasten-was-self-hosted


Here are their concerns in a nutshell:
- Fasten Lighthouse is a completely stateless application
- Theres no way to determine how many users are associated with the same Fasten installation (container/desktop app)
    - **FEAR**: a Fasten self-hoster may offer their server publicly, providing  access to a large number of users  without having to agree to or follow the privacy policy and terms of use that I shared with the provider to get API credentials.
- Fasten Lighthouse doesn’t(cant?) do any validation that it’s redirecting to an “official” Fasten application
    - **FEAR**: a completely separate application could use Fasten Lighthouse with their app, completely ignoring the audit and security review process that the Provider has in place for vetting new applications.

Both of these concerns are completely valid, given the 10’s of millions of healthcare records some of these Healthcare providers protect.
