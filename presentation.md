# Identity & Authorisation — A Primer

> Sixty years of asking *"who are you?"* and *"what may you do?"* — and how we got here.

The gateway deck for the **Identity & Access** and **Authorisation** series. No code, no RFCs in the body, the whole field on one map.

---

## 1. Topics

**The story** — Why identity exists at all · AuthN vs AuthZ · Four eras: mainframe → web → mobile/cloud → agent & wallet · The threat landscape that shaped each era's primitives.

**The vocabulary** — Principal · credential · token · scope · audience · claim · IdP · RP · PEP · PDP · PIP · PAP · north-south vs east-west · federation, delegation, impersonation.

**The map** — Standards landscape (IETF / OIDF / OASIS / W3C / FIDO / NIST / CNCF) · AuthN conceptual map · AuthZ conceptual map · build vs buy.

**The roadmap** — Legal & regulatory backdrop · how the eleven decks fit together · reading order by role and goal · three sentences you can quote.

---

## 2. Why Identity Exists at All — The Original Problem

A computer for one user has no need for identity. The moment a second user shares the machine — or the network — three problems appear at once:

1. **Tell us apart** → Authentication (AuthN) — passwords, passkeys, SAML, OIDC.
2. **Limit damage we can do** → Authorisation (AuthZ) — scopes, RBAC, ABAC, ReBAC, OPA.
3. **Record who did what** → Audit / non-repudiation — syslog, CAEP, SSF, audit pipelines.

Saltzer & Schroeder (1975) already named all three. We've been building tools to honour them ever since.

---

## 3. The Defining Pair — AuthN vs AuthZ

**Authentication (AuthN) — "who are you?"**
- Input: a credential — password, OTP, biometric, signing key, certificate.
- Output: a verified *claim* — `"this principal is alice@example.com"` (or `"this workload is spiffe://prod/orders"`).
- Failure mode: **impersonation** — someone proves to be you who isn't.
- Standards owners: FIDO Alliance, IETF, W3C, OIDF, NIST.

**Authorisation (AuthZ) — "what may you do?"**
- Input: the verified principal + an action + a resource + (often) context (time, IP, risk score).
- Output: a binary decision — *permit* / *deny* — plus an audit-ready reason.
- Failure mode: **privilege escalation** — doing something you weren't permitted to do.
- Standards owners: OASIS (XACML), CNCF (OPA, OpenFGA), AWS / GCP / Azure, Cedar.

**Three concepts that live between them**
- **Federation** — one IdP authenticates, many RPs trust the result. SAML, OIDC, OpenID Federation 1.0.
- **Delegation** — Alice lets an app act *on her behalf* with a narrowed scope. OAuth's whole reason for existing.
- **Impersonation** — a service acts *as* a user (lossless). Token Exchange (RFC 8693). Logged carefully.

**Why the confusion is fatal**
Many real incidents — Capital One 2019, Optus 2022, Microsoft Storm-0558 2023 — start because someone treated *"the request authenticated successfully"* as if it implied *"the request was authorised"*. It does not.

> *"AuthN is the bouncer at the door. AuthZ is the wristband that says which rooms you can enter. Audit is the CCTV that says where you actually went."*

---

## 4. A Brief History I — The Mainframe & Network Era (1961-1995)

| Year | Event | Significance |
|------|-------|--------------|
| 1961 | MIT CTSS | First password file |
| 1975 | Saltzer & Schroeder | "Least privilege" and "fail-safe defaults" named |
| 1978 | Needham-Schroeder | Tickets, replay attacks identified |
| 1988 | Kerberos v4 (MIT) | Trusted third party at scale |
| 1993 | LDAP / X.500 | Directory as a service |
| 1994 | SSL 2.0 (Netscape) | Credentials over the public web |
| 1995 | Windows NT / Domain Controller | Enterprise SSO arrives |

**What was solved:** "tell users on this *system* apart" → "tell users on this *network* apart" via tickets and shared secrets.
**What hadn't been:** identity across organisations. Each company was its own island; trust did not cross boundaries.
**Primitives still in use:** password hash, ticket, directory entry, CA-issued certificate, the *principal* as a first-class object.

---

## 5. A Brief History II — The Web & Federation Era (1995-2014)

| Year | Event | Significance |
|------|-------|--------------|
| 2002 | SAML 1.0 | XML federation |
| 2005 | SAML 2.0 | The enterprise SSO standard |
| 2007 | OAuth 1.0 | Stop sharing passwords |
| 2010 | JWT (Internet-Draft) | Signed JSON tokens |
| 2012 | OAuth 2.0 (RFC 6749) | Bearer tokens, grant types |
| 2013 | SCIM 2.0 | Cross-org user provisioning |
| 2014 | OIDC Core 1.0 | "Sign in with Google" |

**What was solved:** identity *across organisations*. Users sign in once at their IdP and reach hundreds of relying parties.
**What hadn't been:** phishing-resistant credentials, mobile-first flows, machine-to-machine identity, anti-replay token binding.
**Primitives still in use:** SAML assertion, JWT, OAuth grant types, scopes, IdP / RP / Resource-Server triad, SCIM as the provisioning standard.

---

## 6. A Brief History III — Mobile, Cloud & Zero Trust (2014-2023)

| Year | Event | Significance |
|------|-------|--------------|
| 2014 | FIDO U2F · BeyondCorp paper | Phishing-resistant; "Zero Trust" coined |
| 2015 | PKCE (RFC 7636) | OAuth for mobile/SPAs |
| 2018 | SPIFFE/SPIRE · OPA | Workload identity · Policy-as-Code |
| 2019 | WebAuthn L1 · NIST 800-207 | Passkey foundation; ZT architecture |
| 2021 | Zanzibar paper · OpenFGA | ReBAC at planet scale |
| 2022 | Passkeys (sync) | Apple/Google/MS commit |
| 2023 | DPoP · Cedar · OAuth 2.1 | Sender-bound tokens · ABAC engines |

**What was solved:** phishing (passkeys), workload-to-workload identity (SPIFFE), policy as code (OPA / Rego), mobile-safe OAuth (PKCE).
**What hadn't been:** user-controlled identity (your wallet, not the IdP's database), AI agents acting on your behalf, cross-border country-scale federation.
**Primitives still in use:** WebAuthn credential, X.509 SVID, OPA bundle, Cedar policy, the policy-decision-point pattern, mTLS-everywhere east-west.

---

## 7. A Brief History IV — The Agent & Wallet Era (2024-now)

| Date | Event | Significance |
|------|-------|--------------|
| 2024-05 | eIDAS 2.0 enacted | EUDI Wallet mandated |
| 2024-09 | OpenID Federation 1.0 | Trust chains for SIOPv2 |
| 2024-11 | MCP launched | Agents need authorisation |
| 2025-06 | MCP authz profile | OAuth + Resource Indicators |
| 2025-Q4 | FAPI 2.0 final | Finance-grade OIDC baseline |
| 2026-08 | EU AI Act enforced | Agent identity & audit |
| 2026-Q4 | EUDI Wallet live | All 27 member states |

**What's being solved:** citizen-controlled identity. Selective disclosure (prove you're over 18 without revealing your DOB). Agent delegation with a paper trail.
**What's still open:** cross-jurisdiction wallet trust, agent *liability* models, agent-to-agent delegation, regulator's audit grammar for AI systems.
**New primitives:** Verifiable Credential, mDoc, SIOPv2 wallet, OpenID4VCI/VP, agent-as-principal, MCP-resource *audience*, signed agent action logs.

---

## 8. The Threat Landscape — What All These Specs Defend Against

| Threat | What it means | Defence(s) | Covered in |
|--------|---------------|------------|------------|
| Phishing | User typed a real password into a fake login page | WebAuthn / passkeys (origin-bound) | Authentication Methods |
| Credential stuffing | Leaked password + bot tries it on every site | Argon2id, breach lookups, rate limit, MFA | Authentication Methods |
| Token theft & replay | Bearer JWT exfiltrated → attacker uses it | DPoP, mTLS-bound tokens, short TTL, rotation | Adv. OIDC · Edge AuthZ |
| Confused deputy | Token meant for service A used at service B | Resource Indicators (RFC 8707), audience claim, downscope | OAuth · OIDC · Edge AuthZ |
| Lateral movement | Pivot across services after first compromise | SPIFFE workload identity, mTLS east-west, ABAC at every hop | Workload Identity AuthZ |
| Privilege escalation | Authenticated user does what they shouldn't | Least privilege, RBAC → ABAC → ReBAC, central PDP, audit | Authorization Models |
| SAML XSW / alg confusion | Forged assertion / `alg:none` JWT accepted | Strict signature validation, pinned algorithms, FAPI baseline | SAML & SCIM · Adv. OIDC |
| Session hijack via subdomain XSS | Cookie / token leaked from a less-secure subdomain | HttpOnly, SameSite, scoped cookies, CSP, separate origins | Authentication Methods |
| Supply-chain compromise | Attacker patches your dependency / image / IaC | Sigstore, SLSA, signed SBOMs, provenance attestation | Cloud Security · Workload Identity |
| Agent prompt injection | Hostile data steers an LLM agent to misuse a tool token | Per-tool scoped tokens, audience, human-in-the-loop, CAEP signals | OAuth for MCP · Edge AuthZ |

---

## 9. The Standards Landscape — Who Owns What

| Body | Owns |
|------|------|
| **IETF** | OAuth 2.0/2.1, JWT (7519), DPoP (9449), Token Exchange (8693), PKCE (7636), PAR (9126), JAR (9101), Resource Indicators (8707), JWS / JWE |
| **OIDF** (OpenID Foundation) | OpenID Connect Core, FAPI 1/2, Federation 1.0, SIOPv2, OpenID4VCI, OpenID4VP, SSF / CAEP, MODRNA, RISC |
| **OASIS** | SAML 2.0, XACML, WS-Security, WS-Federation |
| **W3C** | WebAuthn (L3), Verifiable Credentials (VC 2.0), DIDs, CredentialManagement |
| **FIDO Alliance** | U2F, FIDO2 / CTAP, MDS, passkey UX guidance |
| **ISO/IEC** | ISO 18013-5/-7 (mDL), ISO/IEC 23220 (mobile eID), ISO 29115 (assurance) |
| **NIST** | SP 800-63 (Digital Identity, IAL/AAL/FAL), SP 800-207 (Zero Trust), FIPS 201 (PIV) |
| **CNCF** | SPIFFE/SPIRE, OPA / Rego, OpenFGA, Cilium, Falco |
| **EU bodies** | eIDAS 2.0, EUDI Wallet ARF, GDPR / DORA |
| **Vendor / cloud** | AWS IAM & Cedar, Google IAM & Zanzibar, Microsoft Entra, Apple/Google passkey ecosystems, Anthropic MCP authz profile |

**Reading the body tells you the politics.** IETF specs are tight, narrow, often grumpy and security-driven. OIDF specs are *profiles* — they say "use these RFCs together, with these constraints". OASIS is enterprise / XML legacy. W3C and FIDO own the *browser* contract. NIST and ISO own the *regulator's* contract. Cloud vendors and CNCF projects move fastest but break compatibility.

---

## 10. The AuthN Conceptual Map

- **Factors** — knowledge (password, PIN), possession (TOTP, push, passkey, smartcard), inherence (fingerprint, face, voice). NIST AAL1 / AAL2 / AAL3.
- **Methods (modern)** — password + Argon2id + breach check; TOTP / push (RFC 6238 / OOB); WebAuthn / FIDO2 / Passkey (origin-bound, phishing-proof).
- **Federation protocols** — SAML 2.0 (enterprise legacy); OIDC + JWT (modern web/mobile); SCIM 2.0 (provisioning); OpenID Federation 1.0 (Sep 2024).
- **Workload identity** — SPIFFE / SPIRE → SVIDs (X.509 or JWT); IRSA (AWS) · GCP WI · Azure WI · WIF; K8s ServiceAccountTokenVolumeProjection. *No passwords for machines — attest, then trust.*
- **User-held credentials (wallet era)** — SIOPv2 (wallet as the IdP); OpenID4VCI / OpenID4VP (issue + present); ISO mDL · Verifiable Credentials. *Selective disclosure, no IdP phone-home.*

Each row covered in detail by a deck: Authentication Methods · OAuth (Primer / Intro / MCP) · OIDC (Intro / Adv) · SAML & SCIM · Workload Identity AuthZ.

---

## 11. The AuthZ Conceptual Map

**Models — the arc:** DAC (owner sets ACL) → MAC (labels + clearances) → RBAC (roles → permissions) → ABAC (attrs + context) → ReBAC (relationship tuples). Each step adds context the previous couldn't express.

**Engines — Policy-as-Code:**
- **OPA / Rego** — general PDP, sidecar / library.
- **Cedar (AWS)** — analyzable, ABAC + RBAC.
- **OpenFGA / SpiceDB** — Zanzibar-style ReBAC.
- **Cloud IAM evaluators** — AWS / GCP / Azure proprietary.
- **Casbin** — embedded library.

**Topologies — where the decision runs:**
- **North-South** — at the edge — API GW, Envoy `ext_authz`, Cloudflare Access.
- **East-West** — in the mesh — Istio AuthorizationPolicy, Linkerd, Cilium.
- **In-app** — in business code — domain-aware checks, OPA library.
- **In the data** — RLS / row-level — Postgres RLS, Snowflake row-access policies.

Decks: Authorization Models · Workload Identity AuthZ · Edge & Gateway AuthZ.

---

## 12. North-South vs East-West — The Two Axes

Once a request enters your system, every authorisation decision falls into one of two camps. Different threat models, different latency budgets, different identity carriers, almost always different teams. Confusing the two is a top-three cause of edge bugs.

**North-South — at the edge**
- Identity carrier: JWT / cookie / OAuth bearer / mTLS client cert.
- Threats: phishing, token theft, replay, confused deputy, scraping.
- Latency: ~5-30 ms acceptable; can call out to introspection.
- Decks: *Edge & Gateway AuthZ*, *OAuth for MCP*.

**East-West — inside the mesh**
- Identity carrier: SPIFFE SVID (X.509 or JWT), mesh mTLS.
- Threats: lateral movement, supply-chain compromise, blast-radius.
- Latency: sub-millisecond; decisions must be local (sidecar).
- Decks: *Workload Identity & Service-Mesh AuthZ*.

---

## 13. Build vs Buy — The Provider Landscape

**Buy — IDaaS:** Auth0, Okta, Microsoft Entra, Stytch, WorkOS, Clerk, AWS Cognito, Firebase Auth, FusionAuth, Descope. *Best when:* you need SOC 2 / FedRAMP inheritance fast, B2B SAML/SCIM out of the box, login isn't your differentiator. Cost scales per MAU.

**Self-host — open source:** Keycloak (Red Hat, Java), ZITADEL (Go, multi-tenant), Authentik (Python), Ory (Hydra/Kratos/Keto, Go), Authelia, Logto. *Best when:* data residency / sovereignty is a hard requirement, MAU economics break commercial, or you need deep customisation. You own the on-call.

**Build — almost never:**
- Roll-your-own SAML / OIDC: don't.
- Roll-your-own session cookies: maybe.
- Roll-your-own AuthZ inside business code: yes — but use OPA / Cedar / OpenFGA underneath.

The trap: identity protocols look simple and aren't. Spend the first year on your product, not on JWT validation edge cases.

**A useful split:** **AuthN + federation = buy.** Login is largely a solved, commoditised, and highly-attacked surface — leverage someone whose only job is keeping it correct. **AuthZ = build, on a policy engine.** Authorisation is your business logic — what your users may do is unique to your product. Use a PDP (OPA / Cedar / OpenFGA), keep policies in your repo, and treat the engine as a library, not a product.

---

## 14. The Legal & Regulatory Backdrop

| Regulation | Force date | What it requires | Standards / specs it produced |
|------------|------------|------------------|-------------------------------|
| **GDPR** (EU) | 2018-05 | Lawful basis for PII; right to erasure; pseudonymous IDs preferred | OIDC pairwise subjects, SCIM delete semantics, ID-token minimisation |
| **PSD2 SCA** (EU) | 2019-09 | Strong customer authentication for online payments; dynamic linking | FAPI 1.0, then FAPI 2.0; OBIE / Berlin Group profiles |
| **HIPAA** (US) | 2003 (still) | Audit trail, MFA for PHI, BAA contracts; minimum necessary access | SAML in healthcare, SMART on FHIR (OAuth profile) |
| **CCPA / CPRA** (CA) | 2020 / 2023 | Opt-out of sale, right to know, right to delete | GPC header, SCIM delete cascade, identity-graph minimisation |
| **eIDAS 2.0** (EU) | 2024-05 | Every citizen must use a state-recognised digital wallet | EUDI Wallet ARF, OpenID4VCI / VP, ISO mDL, SD-JWT |
| **DORA** (EU finance) | 2025-01 | Operational resilience; ICT third-party risk; incident reporting in hours | FAPI 2.0 baseline, OpenID Federation 1.0 trust chains |
| **EU AI Act** | 2026-08 | Identity, log, and audit "high-risk" AI systems and their actions | MCP authz profile, agent-as-principal patterns, signed action logs |
| **SOC 2 / ISO 27001** | continuous | Access reviews, MFA, audit logs, least privilege, joiner-mover-leaver | SCIM provisioning, RBAC/ABAC reviews, CAEP / SSF event streams |

**The pattern:** regulators set a behaviour requirement → standards bodies (OIDF, IETF, W3C, ISO) wire a protocol → vendors and OSS projects ship products. Three-step flow, every time. Watch the regulators to know what's coming next.

---

## 15. How To Read This Series — Eleven Decks, One Map

**Identity & Access — "who"**
0. *(you are here)* Identity & Authorisation Primer
1. Authentication Methods — passwords, MFA, passkeys, recovery
2. OAuth — A Gentle Primer (Part 0)
3. Introduction to OAuth (Part 1) — the protocol
4. OAuth for MCP Servers (Part 2) — agents + provider zoo
5. Introduction to OpenID Connect — IDs on top of OAuth
6. Advanced OpenID Connect — FAPI 2.0, Federation, EUDI
7. SAML 2.0 & SCIM — the enterprise stack

**Authorisation — "what may"**
8. Authorization Models — RBAC / ABAC / ReBAC, Policy-as-Code
9. Workload Identity & Service-Mesh AuthZ — east-west
10. Edge & Gateway AuthZ — north-south

**Reading order by goal**
- *"I'm building a SaaS login":* 1 → 2 → 3 → 5 → 7 → 8
- *"I'm hardening an MCP / agent":* 2 → 3 → 4 → 10
- *"I'm an SRE wiring a mesh":* 9 → 10 → 8
- *"I'm in B2B / enterprise":* 7 → 5 → 6 → 8
- *"I'm preparing for EU AI Act / EUDI":* 6 → 4 → 10 → §14 above

---

## 16. Take-aways

1. **AuthN and AuthZ are different decisions, computed by different code, against different sources.** Most real incidents come from confusing them.
2. **The whole field is sixty years of moving identity outward** — from a file on one machine, to a network ticket, to a federated assertion, to a user-held wallet credential, to an AI agent's token.
3. **Buy AuthN, build AuthZ on a policy engine.** Login is commoditised; what users may do is your business logic.

**Three things to do next:**
- Open *Authentication Methods* (deck 1) and look at the AAL ladder — it tells you what "secure enough" means in your domain.
- Run a one-pager that lists, for each user-facing entry point you own: *who validates the token? who decides the action? where is it logged?*
- Pick one authoriser in your stack and ask which threat from §8 it actually mitigates. If the answer is "I'm not sure", you've found a deck to read.

---

## Canonical references

- Saltzer & Schroeder, *"The Protection of Information in Computer Systems"* (1975)
- NIST SP 800-63-4 (Digital Identity Guidelines)
- NIST SP 800-207 (Zero Trust Architecture)
- OWASP API Security Top 10 (2023)
- OWASP ASVS v5.0 (Application Security Verification Standard)
- Aaron Parecki, *"OAuth 2.0 Simplified"*
- Justin Richer & Antonio Sanso, *"OAuth 2 in Action"*
- Google *"BeyondCorp"* papers (2014-2017)
- Google *"Zanzibar"* paper (USENIX 2019)
- eIDAS 2.0 + EUDI Wallet ARF v1.4

---

*Companion decks in the series: see [Software](https://github.com/BrendanJamesLynskey/Software).*
