# Liquid

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

Liquid (**liquid.trade**, formerly tryliquid.xyz) is a perpetual-futures trading platform and perp-DEX
aggregator. Traders go long or short on 500+ markets — crypto perps, US and international equities,
commodities, FX, indices, pre-IPO names like OpenAI, Anthropic and SpaceX, and event/prediction contracts
— 24/7 with up to 50x multipliers, routed through venues including Hyperliquid, with funds held in the
user's own non-custodial wallet.

Liquid raised an **$18M Series Seed** led by Neo and Left Lane Capital in April 2026, following a $7.6M
seed led by Paradigm.

## Programmable surface

Liquid publishes **no public REST API and no OpenAPI**. Its entire programmable surface is **Co-Invest**,
a published remote **MCP server** at `https://coinvest.liquid.trade/mcp` that puts market research,
portfolio state and confirmed trade execution inside Claude, ChatGPT, Cursor, iMessage and any
MCP-compatible client.

- OAuth 2.1 — authorization code + PKCE (S256) + dynamic client registration, with RFC 8414 and RFC 9728
  discovery documents live on the MCP host.
- Two scopes: `read` and `trade`. The grant can never withdraw funds or change account settings.
- Every state-changing action renders a confirmation card; nothing executes without a human tap.
- Paper mode: a simulated $10,000 balance against live market data.

## Artifacts

| Dir | Artifact |
|---|---|
| `mcp/` | Co-Invest MCP server manifest (searched) |
| `well-known/` | RFC 9728 + RFC 8414 metadata, saved verbatim |
| `llms/` | `llms.txt` from docs.liquid.trade, saved verbatim |
| `authentication/` | OAuth 2.1 profile |
| `scopes/` | `read` / `trade` scope reference |
| `conventions/` | MCP transport, confirmation model, limits, error shape |
| `conformance/` | Standards conformance + Zellic audit record |
| `sandbox/` | Paper-trading mode |
| `changelog/` | Daily dated changelog |
| `lifecycle/` | Versioning, cadence, support; no status page or deprecation policy published |
| `packages/` | Registry sweep — no first-party SDK exists |
| `security/` | Domain security probe (TLS/HSTS/DNSSEC/CAA/SPF/DMARC) |
| `skills/` | Four Agent Skills for the Co-Invest surface |

Backed by: paradigm, techstars — https://www.liquid.trade
