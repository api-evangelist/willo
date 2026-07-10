# Willo (willo)

Willo is an asynchronous ("one-way") video interviewing and screening platform. Teams invite candidates to record answers to a set of pre-defined questions on any browser or device - no downloads, apps, or login required - and review the responses on a Kanban board. The **Willo Integration API V2** exposes the platform's UI actions as a public REST API so you can embed video interviewing into a job board, ATS, CRM, or staffing platform.

**APIs.json:** [https://raw.githubusercontent.com/api-evangelist/willo/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/willo/refs/heads/main/apis.yml)

## Access Model (Honest Summary)

- **The API reference is public and self-serve.** Willo's full API documentation is openly readable as a [Postman collection](https://documenter.getpostman.com/view/7798010/VUjSEiSn); you do not need to talk to sales to read it.
- **Authentication is by an integration key ("API key").** Each user generates and cycles their own key from the Willo Integrations page at `https://app.willotalent.com/integrations`. The key is sent in the `Authorization` header, and all requests must be over HTTPS.
- **An account is required, and some developer features are tier-gated.** A paid Willo plan (Growth or Scale) provides the account and integration key. Willo's pricing page lists a formal **OpenAPI file**, **SSO**, **dedicated developer support**, and **12+ month data retention** as **Enterprise**-plan features. So the API is documented publicly and usable on self-serve plans, but the deepest developer support and the vendor-provided OpenAPI are Enterprise perks.
- **The `developers.willo.video` developer-portal host did not resolve over HTTPS at review time**; the canonical, working reference is the Postman documenter linked above.

## Base URL and Environments

- **Production:** `https://api.willotalent.com/api/integrations/v2`
- **Staging:** `https://api.stage.willotalent.com/api/integrations/v2`

Endpoint paths, HTTP methods, authentication, status codes, and webhook triggers are **confirmed** from Willo's published Postman reference. The request/response **body schemas** in the OpenAPI in this repo are **modeled** from Willo's documented resource glossary and are illustrative - confirm exact field names against the live reference before production use.

## Tags

- Video Interviewing
- Recruitment
- HR Tech
- ATS
- Screening
- Async Video

## Timestamps

- **Created:** 2026-07-10
- **Modified:** 2026-07-10

## APIs

All of the logical APIs below are the same Willo Integration API V2 under one base URL; they are split by resource for discovery.

### Willo Interviews API

Create, list, retrieve, update, and delete interviews - the named sets of pre-defined questions a candidate answers (typically a "job" in an ATS). Questions (prompt, answer type, duration, retakes, thinking time) are embedded on each interview rather than exposed as a separate endpoint.

- **Base URL:** `https://api.willotalent.com/api/integrations/v2`
- **API Reference:** [Willo Integration API V2 (Postman)](https://documenter.getpostman.com/view/7798010/VUjSEiSn)

### Willo Participants (Candidates) API

Invite candidates ("participants") to an interview, list and retrieve them with their completed video responses, move them between Kanban stages, and read their identity-verification (IDV) details and media. Video responses surface as a sub-resource on the participant, not as a separate endpoint.

### Willo Departments API

Manage departments - sub-divisions of the account, shown as "Companies" in the UI and used to represent brands, geographies, or business units, each configurable with its own branding.

### Willo Webhooks API

Subscribe third-party endpoints to Willo event triggers - **New Response**, **Stage Change**, **New Comment**, and **New Score** - and manage those subscriptions. Willo recommends webhooks over polling for change tracking.

### Willo Message Templates API

Manage the invite, reminder, and success email/SMS templates that Willo sends to participants.

### Willo Users API

Invite, list, retrieve, update, and remove account users across the Owner, Admin, and Standard roles.

### Willo Interview Templates API

Browse Willo's pre-built interview template library and its categories, retrieve a template with its questions, and create a ready-to-use interview directly from a template.

### Willo Child Organisations API

Create and list child organisations under a parent organisation - for agencies, resellers, or multi-brand groups.

## Webhook Event Triggers

- **New Response** - a new interview response is received from a participant.
- **Stage Change** - a participant is moved to a different stage on the Willo Kanban board.
- **New Comment** - a participant receives a comment from a member of the hiring team.
- **New Score** - a participant receives a score from a member of the hiring team.

## Rate Limits

Willo throttles the API but does not publish a fixed numeric request rate. It warns against continuous polling, repeated job/response scans, and concurrent bursts, and recommends using webhooks for change tracking. Throttled requests return HTTP 429. See [`rate-limits/willo-rate-limits.yml`](rate-limits/willo-rate-limits.yml).

## Plans and Pricing

Subscription tiers (headline USD): **Growth** $279/mo ($209/mo annual, up to 4 users, 2 assessments), **Scale** $409/mo ($307/mo annual, up to 20 users, 10 assessments, custom scorecards/branding, 6-month retention), and a custom **Enterprise** plan (unlimited users/assessments, SSO, OpenAPI, dedicated developer support). A 50% non-profit discount is available. See [`plans/willo-plans-pricing.yml`](plans/willo-plans-pricing.yml).

## Common Properties

- [LinkedIn](https://www.linkedin.com/company/willovideo)
- [Website](https://www.willo.video/)
- [Documentation (Postman)](https://documenter.getpostman.com/view/7798010/VUjSEiSn)
- [Developer Portal](https://developers.willo.video/)
- [Sign Up / Integrations](https://app.willotalent.com/integrations)
- [Support](https://support.willo.video/)
- [Status Page](https://status.willo.video/)
- [Changelog](https://feedback.willo.video/changelog)
- [Plans](plans/willo-plans-pricing.yml)
- [Rate Limits](rate-limits/willo-rate-limits.yml)
- [Fin Ops](finops/willo-finops.yml)

## Review

Does Willo expose a documented public WebSocket API? **No.** The public Willo Integration API V2 is request/response REST over HTTPS; real-time change delivery is handled by outbound webhooks, not a server-push socket. No AsyncAPI document was created. See [`review.yml`](review.yml).

## Maintainers

**FN:** Kin Lane
**Email:** kin@apievangelist.com
