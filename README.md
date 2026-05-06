# 🪪 Identity & Authorisation — A Primer

An interactive Reveal.js presentation: the gateway deck for the **Identity & Access** and **Authorisation** series. Sixty years of asking *"who are you?"* and *"what may you do?"* — and how we got here. No code, no RFCs in the body, the whole field on one map.

## ▶ [Open the Presentation](https://brendanjameslynskey.github.io/Identity_and_Authorisation_Primer/)

## 📄 [Markdown Version](presentation.md)

## 📚 The series

**Identity & Access (AuthN)** — [Authentication Methods](https://brendanjameslynskey.github.io/Authentication_Methods/) · [OAuth Primer](https://brendanjameslynskey.github.io/OAuth_Primer/) · [Introduction to OAuth](https://brendanjameslynskey.github.io/Introduction_to_OAuth/) · [OAuth for MCP Servers](https://brendanjameslynskey.github.io/OAuth_for_MCP/) · [Introduction to OpenID Connect](https://brendanjameslynskey.github.io/Introduction_to_OpenID_Connect/) · [Advanced OpenID Connect](https://brendanjameslynskey.github.io/Advanced_OpenID_Connect/) · [SAML 2.0 & SCIM](https://brendanjameslynskey.github.io/SAML_and_SCIM/)

**Authorisation (AuthZ)** — [Authorization Models](https://brendanjameslynskey.github.io/Authorization_Models/) · [Workload Identity & Service-Mesh AuthZ](https://brendanjameslynskey.github.io/Workload_Identity_AuthZ/) · [Edge & Gateway AuthZ](https://brendanjameslynskey.github.io/Edge_and_Gateway_AuthZ/)

---

## Contents

| # | Topic | Description |
|---|-------|-------------|
| 01 | Title | Story · Vocabulary · Map · Roadmap |
| 02 | Topics | The four panels of the primer |
| 03 | Why Identity Exists at All | The original three-problem multi-user picture |
| 04 | The Defining Pair | AuthN vs AuthZ, with federation / delegation / impersonation between them |
| 05 | History I — Mainframe & Network | 1961-1995 · CTSS, Saltzer-Schroeder, Kerberos, LDAP, SSL |
| 06 | History II — Web & Federation | 1995-2014 · SAML, OAuth, JWT, SCIM, OIDC |
| 07 | History III — Mobile, Cloud & Zero Trust | 2014-2023 · FIDO2, BeyondCorp, SPIFFE, OPA, passkeys, DPoP |
| 08 | History IV — Agent & Wallet Era | 2024-now · eIDAS 2.0, EUDI, MCP, FAPI 2.0, EU AI Act |
| 09 | The Threat Landscape | Ten attack classes mapped to defences and decks |
| 10 | The Standards Landscape | IETF · OIDF · OASIS · W3C · FIDO · NIST · CNCF · EU · cloud vendors |
| 11 | The AuthN Conceptual Map | Factors → methods → federation → workload → wallet |
| 12 | The AuthZ Conceptual Map | Models (DAC→ReBAC) · engines · topologies |
| 13 | North-South vs East-West | The two axes of authorisation, with diagram |
| 14 | Build vs Buy | IDaaS providers · open-source self-host · roll-your-own |
| 15 | The Legal & Regulatory Backdrop | GDPR · PSD2 · HIPAA · CCPA · eIDAS 2.0 · DORA · EU AI Act · SOC 2 |
| 16 | How To Read This Series | Eleven decks, reading order by goal and by role |
| 17 | Take-aways & References | Three sentences plus the canonical bibliography |

---

## Audience

- **Engineers, SREs, architects, founders** new to the identity/authorisation field who want a single map before drilling into specs.
- **Anyone about to read the rest of this series** and wanting the vocabulary, history, and threat-model context up front.
- **PMs / TPMs / compliance** who need to understand *why* the protocol zoo exists and where the regulatory pressure is coming from.

The deck deliberately contains no RFC numbers in the body, no code, and no JSON. Those start in the topic-specific decks linked above.

## Slide Controls

| Action | Key |
|--------|-----|
| Next / Previous | `→` `←` or swipe |
| Overview | `Esc` |
| Fullscreen | `F` |
| Export to PDF | Append `?print-pdf` to URL, then print |

## Technology

[Reveal.js 4.6](https://revealjs.com) · Playfair Display + DM Sans + JetBrains Mono · inline SVG diagrams.

Single self-contained `index.html` — no build step, no npm, no dependencies to install.

## See also

The full eleven-deck Identity & Access + Authorisation series, indexed from the [Software](https://github.com/BrendanJamesLynskey/Software) repository.

Companion technical decks: [Cloud `*aaS` 05 — Cloud Security](https://github.com/BrendanJamesLynskey/Cloud_aaS_05_Cloud_Security) · [Docker for LLMs, Agents & MCP](https://github.com/BrendanJamesLynskey/Docker_for_LLMs_and_Agents) · [Introduction to Web Authentication](https://github.com/BrendanJamesLynskey/Introduction_to_Web_Authentication).

## License

Educational use. Diagrams and examples provided as-is.
