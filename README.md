# Trusona

<!-- API-EVANGELIST-PROVENANCE:BEGIN -->
> ### About this repository
>
> **This is not our API.** This repository is an independent, third-party profile of a company's
> **publicly available** API surface, maintained by [API Evangelist](https://apievangelist.com).
> API Evangelist does not operate, host, resell, or support this company's APIs, and is not
> affiliated with or endorsed by the company unless stated on the profile.
>
> **Where the information came from.** Everything here is assembled from material a member of the
> public can reach with a browser and no credentials — the company's own website, developer portal
> and documentation, the specifications it publishes for public use (OpenAPI, AsyncAPI, JSON Schema,
> `apis.json`, `llms.txt` and similar), its public repositories, and its public status, pricing and
> changelog pages. **Nothing here is obtained by breaching a system, defeating an access control, or
> using credentials of any kind.**
>
> **The rating is an independent assessment.** The Kin Score and Agent Readiness rating are
> independently calculated scores of a company's *public* API artifacts, produced by API Evangelist
> against a published rubric. They are not certifications, endorsements, security assessments, or
> audits, and they score published artifacts — not the quality, safety, or security of the software.
>
> **Corrections, re-scores, and removal are free.** No partnership, contract, or purchase is
> required, and you do not need to justify the request.
>
> - **Something wrong?** Open an issue on this repository, or email
>   [info@apievangelist.com](mailto:info@apievangelist.com).
> - **Published something new?** Ask for a re-score and we will re-run the rating.
> - **Want the listing taken down?** Say so and we will honor it. The profile is reduced to your
>   company name, a factual description, and a link to your own site, and the company is recorded as
>   **unrated** — never scored zero for having asked.
>
> **Response times.** Acknowledgement within **one business day**; removal or restriction within
> **two business days**; corrections and re-scores within **five business days**.
>
> **Not from the company, and here with a question?** You are welcome here — we would rather be the
> front line and point you the right way than have a good report go nowhere. What this repository
> can answer is narrow, though, so it is worth knowing who you are actually looking for:
>
> - **A question about how the API works, an account, billing, or a bug in the service** — that is
>   the company's own support, not us. We profile this API; we do not operate it and cannot see
>   your account.
> - **A bug in an open-source project we only catalog** — file it on that project's own repository.
>   This has happened with a real and correct bug report that reached us instead of the people who
>   could fix it, which helped nobody.
> - **Anything about this listing itself** — the description, the tags, the rating, a missing or
>   wrong artifact — is ours. Open an issue here.
> - **Not sure, or something general about API Evangelist or APIs.io** — open an issue on the
>   [APIs.io Inbox](https://github.com/api-search/inbox) and we will route it.
>
> **This repository contains no software, and we will never ask you to download anything.** There is
> no build, release, installer, or binary here — only text and machine-readable API descriptions, so
> there is nothing here that can be "corrupt" or need "repairing". Any issue, comment, or email
> claiming otherwise and offering a download link is not from us and is hostile. Do not follow the
> link; it is a lure. Report it to GitHub and, if you like, tell us at
> [info@apievangelist.com](mailto:info@apievangelist.com) so we can take it down.
>
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

Trusona is a Scottsdale, Arizona identity impersonation detection company founded in 2015 by fraud-prevention expert Ori Eisen. Its ATO Protect suite verifies that the person behind a help-desk call, account-recovery request, MFA reset, HR onboarding or wire approval is really who they claim to be — checking a government-issued ID against authoritative sources such as State DMVs over the AAMVA network and layering SIM-swap/port-out detection, patented man-in-the-middle detection and anti-replay technology, deliberately without a liveness selfie.

## API surface

| API | Contract | Base URL |
| --- | --- | --- |
| ATO Protect Verification API (v2.2.0) | [OpenAPI 3.1](openapi/trusona-verification-api-openapi.yml) | `https://authcloud.trusona.net` |
| Driver License Verification API (v1.0.0) | [OpenAPI 3.1](openapi/trusona-driver-license-verification-api-openapi.yml) | `https://authcloud.trusona.net` |
| ID Proofing API (v2, AAMVA) | documented on the website, no OpenAPI | provisioned per tenant |

- Website — https://www.trusona.com/
- Integrations / developer entry point — https://www.trusona.com/integrations
- API reference — https://authcloud.trusona.net/docs/index.html
- Status — https://status.trusona.com/
- Trust center — https://trust.trusona.com/
- GitHub — https://github.com/trusona

Trusona publishes its own [`llms.txt`](llms/trusona-llms.txt) and an Apache-2.0
[Agent Skill](skills/_index.yml) for the ATO Protect APIs
([github.com/trusona/atop-agent-skill](https://github.com/trusona/atop-agent-skill)), both
mirrored here verbatim. It publishes no MCP server and no A2A agent card.

> **Note on a previous version of this profile.** This repository was seeded from a harvest
> backlog whose `Website` pointer was a secondary-market listing venue
> (`nasdaqprivatemarket.com`) rather than Trusona's own site. That was a harvest artifact, not
> a fact about the company, and it has been corrected.
