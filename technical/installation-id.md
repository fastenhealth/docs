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
    - **FEAR**: a Fasten self-hoster may offer their server publicly, providing  access to a large number of users  without having to agree to or follow the privacy policy and terms of use that I shared with the provider to get API credentials.
- Fasten Lighthouse doesn’t(cant?) do any validation that it’s redirecting to an “official” Fasten application
    - **FEAR**: a completely separate application could use Fasten Lighthouse with their app, completely ignoring the audit and security review process that the Provider has in place for vetting new applications.

Both of these concerns are completely valid, given the 10’s of millions of healthcare records some of these Healthcare providers protect.

---

After discussing potential solutions with the Providers, here’s what I’m proposing to the community:

- Fasten Self-Hosted could implement an installation ID mechanism, which would be sent along with every request to the Fasten Lighthouse. The Installation ID would be associated with a Fasten Self-Hosted administrator Name + Email address (for contact purposes).
- Fasten Lighthouse could enforce Provider limits for # of registered users per installation ID — in the order of XX rather than XXX (so 10s of users rather than 100’s of users)
- The idea is that if each installation of Fasten Self-Hosted is limited to XX users per Provider, then the fallout of a misconfiguration or malicious application is limited.
- You would only need to register an Installation ID once, and it would basically be another config file. The registration information (Name + Email) would only be used to notify system admins if they’re reaching a user limit for a specific Provider.
- Fasten Lighthouse is **NOT** involved in requesting your medical records from your Provider (that communication is always done directly between your Fasten self-hosted instance and the Provider -- this does not change with this proposal -- only the Auth flow is modified)

---

Obviously this is non-optimal, but the potential for abuse with Lighthouse is a fact that’s come up numerous times with large Providers. None of these providers have ever seen an open-source application like Fasten before, so they're being extra cautious to make sure they're not missing anything.

I’m open to ideas/feedback regarding my proposal (and alternatives!)

Let’s discuss in the dedicated #developers Installation ID Thread: https://discord.com/channels/1023634406935642223/1169976288044388362

---
