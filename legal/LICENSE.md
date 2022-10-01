# LICENSE

## Top Choice

- [MariaDB BSL1.1 license](https://mariadb.com/bsl-faq-adopting/#osl) - used by [ZeroTier](https://github.com/zerotier/ZeroTierOne/blob/master/LICENSE.txt)
  - seems like a way to "safely" release the code, while ensuring that the code is fully open source if the company doesn't go anywhere.  

## Alternatives

> Originally from /u/Kairos8134 's helpful [Reddit comment](https://www.reddit.com/r/selfhosted/comments/xj9rx7/introducing_fasten_a_selfhosted_personal/ip78dhr/)

1. Charging for a hosted service while licensing code using a source-available now / open source later license such as the BSL to limit commercial competition (has a non-commercial clause but reverts to an open source license after a preset period of time) such as [the one used by ZeroTier](https://github.com/zerotier/ZeroTierOne/blob/master/LICENSE.txt).
  - **[PRO]** - Hosted service, every customer would be "paid".
  - **[PRO]** - Agreements with Healthcare providers would be clearer
  - **[CON]** - Have to manage our own infrastructure
  - **[CON]** - Compliance
  - **[CON]** - Users have to Trust us

2. Sponsorware such as is used by [Material for MkDocs](https://squidfunk.github.io/mkdocs-material/insiders/#whats-in-for-me), where there is a private "premium version" where some of the big ticket new features land first but these features are gradually migrated to the publicly available open source project when different funding tiers are reached.
  - **[PRO]** - Users get to self host (Trust-less)
  - **[PRO]** - Users eventually get all features
  - **[CON]** - Coding/coordination is more complicated
  - **[CON]** - Depends on Sponsors to keep the project alive

3. The [Photoprism model](https://github.com/photoprism/photoprism/issues?q=label%3Asponsor-feature) where a certain small subset of "premium" features that are unlocked when a certain level of sponsorship is reached, but all the code (including the premium features) are included in the open project so if someone wants to go through the hassle of compiling it out themselves they are entitled to, but it takes a significant amount of effort (see [this Twitter thread](https://nitter.net/photoprism_app/status/1363795865543077890#m)).
  - **[PRO]** - Users get to self host (Trust-less)
  - **[PRO]** - Users eventually get all features
  - **[CON]** - Licensing/feature flags needs to be designed to enable/disable features.
  - **[CON]** - Depends on Sponsors to keep the project alive

4. The [HomeAssistant model](https://www.nabucasa.com/pricing/) of charging for a hosted service which manages paid connections to commercial entities to provide the service without the hassle of user setup (in the case of Nabu Casa, things like Google Assistant integration)
  - **[PRO]** - Hosted service, every customer would be "paid".
  - **[PRO]** - Agreements with Healthcare providers would be clearer
  - **[CON]** - Have to manage our own infrastructure
  - **[CON]** - Compliance
  - **[CON]** - Users have to Trust us

5. Open source the project, charge for pre-built artifacts
  - **[PRO]** - Open source, users get every feature
  - **[PRO]** - Trust - Users who don't trust us can build their own
  - **[CON]** - Have to manage our own distribution system

6. Cripple-ware - Opensource but unusable without a license, because of Authentication Gateway
  - **[PRO]** - Open source, users get every feature
  - **[PRO]** - Trust - Users who don't trust us can build their own
  - **[PRO]** - every customer would be "paid"
  - **[CON]** - Have to manage our own licensing distribution system
  - **[CON]** - User's cant do much without Gateway access (true for all other models as well)

7. Source Available - on purchase source code is available to users
  - **[PRO]** - users get every feature
  - **[PRO]** - Trust - Users who don't trust us can build their own
  - **[PRO]** - every customer would be "paid"
  - **[CON]** - community of OS users cannot contribute fixes/providers.

8. Common Clause
  - https://commonsclause.com/
